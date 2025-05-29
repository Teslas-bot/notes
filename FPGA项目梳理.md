# 单光束三自由度FPGA程序

## 程序结构

1. MIPI的IP核接收相机数据
2. 对相机数据进行FFT解算出频率
3. 根据频率和组内的公式计算出对应的位移，俯仰角，偏摆角
4. 使用千兆以太网发送相机传输过来的数据。

## FFT代码问题整理

### FFT原理

[快速傅里叶变换(FFT)——有史以来最巧妙的算法？_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1za411F76U/?spm_id_from=333.337.search-card.all.click&vd_source=0c6e9aa27976c7e534f51b25bcdd53f0)

快速傅里叶变换

![image-20250529175930193](FPGA项目梳理.assets/image-20250529175930193.png)

快速傅里叶逆变换

![image-20250529180500414](FPGA项目梳理.assets/image-20250529180500414.png)

![image-20250529180538221](FPGA项目梳理.assets/image-20250529180538221.png)

![image-20250529180213994](FPGA项目梳理.assets/image-20250529180213994.png)

![image-20250529180831077](FPGA项目梳理.assets/image-20250529180831077.png)

![image-20250529181001772](FPGA项目梳理.assets/image-20250529181001772.png)

![image-20250529181109561](FPGA项目梳理.assets/image-20250529181109561.png)

![image-20250529181100971](FPGA项目梳理.assets/image-20250529181100971.png)

![image-20250529181125879](FPGA项目梳理.assets/image-20250529181125879.png)

核心思想：

​	![image-20250529181821275](FPGA项目梳理.assets/image-20250529181821275.png)

1. 利用函数奇偶性，将$P(x)$这个函数分解成奇偶两部分。
2. 对$x$取$\pm$对，将方程组中所需要的的自变量$x$减少一半。出现递归中无法计算的问题
3. 为解决递归中无法计算的问题，使用复数。$x$使用1的n次单位复根。这样保证每次平方完，它们还是正负成对出现的。这个idea利用了单位复根的性质，是FFT的核心思想。
4. IFFT的算法与FFT一模一样，只是自变量$x$的取值需要变化一下。

## 以太网问题整理

### 以太网数据帧格式

不同的协议层对数据包有不同的称谓，在传输层叫做段（segment），在网络层主教座数据包（datagram）,在链路层叫做帧（frame）。数据封装称帧后发到传输介质上，到达目的主机后每层协议再剥掉相应的首部，最后将应用层数据交给应用程序处理。

FCS校验使用CRC校验的方式进行计算。

![img](https://img2023.cnblogs.com/blog/1727351/202308/1727351-20230807094256282-968267180.png)

![Enet007](https://doc.embedfire.com/fpga/altera/ep4ce10_pro/zh/latest/_images/Enet007.png)

### 模块实现思路

使用Verilog实现千兆以太网（1 Gbps）是一个复杂的任务，通常涉及与物理层芯片（PHY）的协同工作，并需要深入理解以太网协议（尤其是IEEE 802.3标准）和数字逻辑设计。以下是实现的核心思路、关键模块和注意事项：

#### **核心思路：**

1.  **分层实现：**
    *   **MAC (Media Access Control) 子层 (Verilog 核心)：** 这是你在FPGA/ASIC中用Verilog实现的主要部分。负责帧的组装/解析、地址识别、错误检测（CRC）、流量控制（可选）、与上层（如CPU或DMA控制器）的接口。
    *   **PHY (Physical Layer) 芯片 (外部器件)：** 负责实际的信号调制解调、线路编码（如8B/10B for SGMII）、时钟恢复、物理介质连接（RJ45/SFP等）。FPGA通过标准接口（如GMII, RGMII, SGMII）与PHY芯片连接。**你通常不需要用Verilog实现PHY功能。**

2.  **接口选择：** FPGA与PHY之间的接口是关键：
    *   **GMII (Gigabit Media Independent Interface)：** 标准接口，8位数据位宽，125 MHz时钟。数据速率 = 8 bits * 125 MHz = 1000 Mbps。时钟由PHY提供。
    *   **RGMII (Reduced GMII)：** 更常用的接口，减少引脚数。4位数据位宽，双沿采样（DDR），125 MHz时钟（上升沿和下降沿都采样）。数据速率 = 4 bits * 2 (DDR) * 125 MHz = 1000 Mbps。需要DDR输入/输出寄存器（IDDR/ODDR）。
    *   **SGMII (Serial GMII)：** 串行接口，通常通过FPGA的Gigabit Transceiver (如Xilinx的GTX/GTH/GTY 或 Intel的Transceiver) 实现。速率是1.25 Gbps（包含8B/10B编码开销）。更高速率（10G+）的基础。

#### **Verilog 实现核心模块 (MAC 层)：**

1.  **顶层模块 (Ethernet_MAC_Top):**
    *   实例化发送模块 (`tx_path`)、接收模块 (`rx_path`)、时钟管理模块（如需要）、PHY接口模块（处理GMII/RGMII/SGMIO逻辑）、控制/状态寄存器（CSR）模块（可选，用于配置和状态监控）。
    *   提供与上层逻辑（如CPU或数据引擎）的接口（如AXI-Stream, Avalon-ST, FIFO接口）。

2.  **发送路径 (tx_path):**
    *   **用户接口 (如 AXIS Slave)：** 接收来自上层的数据包（目的MAC、源MAC、类型/长度、有效载荷）。处理背压（Backpressure）。
    *   **帧组装 (Frame Assembly)：**
        *   添加 **前导码 (Preamble)** 和 **帧起始定界符 (SFD)**：通常是固定的 `8'h55 8'h55 8'h55 8'h55 8'h55 8'h55 8'h55 8'hd5`。
        *   添加 **目的MAC地址 (6字节)** 和 **源MAC地址 (6字节)**。
        *   添加 **长度/类型字段 (2字节)**。
        *   添加 **数据/有效载荷 (46-1500字节)**：如果上层数据不足46字节，需要添加 **填充 (Padding)** 到46字节。
        *   计算并添加 **帧校验序列 (FCS / CRC32)**：对整个帧（从目的MAC到填充结束）计算CRC32（多项式 `0x04C11DB7`，初始值 `0xFFFFFFFF`，输入输出需反转）。可以使用查找表（LUT）或线性反馈移位寄存器（LFSR）在流水线上实时计算。
    *   **IFG (Inter-Frame Gap) 控制：** 在帧之间插入最小12字节（96 bit times）的空闲时间。
    *   **PHY 接口逻辑 (如 GMII_TX)：**
        *   将组装好的帧数据（包括控制信号如 `tx_en`）按照GMII/RGMII时序要求输出。
        *   对于RGMII，需要使用 `ODDR` 原语将4位数据在125MHz时钟的双边沿输出，并生成 `tx_ctl` 信号（`tx_en` XOR `tx_er`）。
        *   处理PHY的流控信号（如 `pause`，如果支持）。

3.  **接收路径 (rx_path):**
    *   **PHY 接口逻辑 (如 GMII_RX)：**
        *   按照GMII/RGMII时序要求接收来自PHY的数据和控制信号（`rx_dv`, `rx_er`）。
        *   对于RGMII，需要使用 `IDDR` 原语在125MHz时钟的双边沿采样4位数据和 `rx_ctl` 信号，并解出 `rx_dv` 和 `rx_er`。需要处理时钟/数据偏移（Skew）。
    *   **帧同步与定界：**
        *   检测 **前导码** 和 **SFD** (`8'hd5`) 来确定帧的开始。丢弃前导码。
    *   **帧解析 (Frame Parsing)：**
        *   提取 **目的MAC地址 (6字节)**。
        *   提取 **源MAC地址 (6字节)**。
        *   提取 **长度/类型字段 (2字节)**。
        *   根据长度/类型字段确定 **数据/有效载荷** 的长度。
        *   接收并存储 **数据/有效载荷**。
        *   接收 **帧校验序列 (FCS / CRC32) (4字节)**。
    *   **CRC 校验 (Error Detection)：**
        *   对接收到的帧（从目的MAC到FCS之前的最后一个字节）实时计算CRC32（使用与发送端相同的算法和多项式）。
        *   将计算得到的CRC32值与接收到的FCS值进行比较。
        *   如果CRC错误或检测到 `rx_er` 信号，则标记该帧为无效。
    *   **帧过滤 (Frame Filtering - 可选但推荐)：**
        *   检查目的MAC地址：是否匹配本机MAC地址、广播地址(`FF:FF:FF:FF:FF:FF`)或本机已加入的组播地址？不匹配的帧可以丢弃（节省上层带宽）。
    *   **用户接口 (如 AXIS Master)：** 将解析后的有效帧（目的MAC、源MAC、类型/长度、有效载荷、帧状态 - 有效/错误）发送给上层逻辑。需要处理上层背压。

4.  **控制/状态寄存器 (CSR - Control and Status Registers) 模块 (可选但实用):**
    *   提供软件（CPU）可访问的寄存器，用于：
        *   配置：本机MAC地址、使能发送/接收、设置流控参数、使能混杂模式（接收所有帧）等。
        *   状态：发送/接收状态、错误计数器（CRC错误、对齐错误、FIFO溢出等）、链路状态（通常从PHY读取）。
    *   通常通过简单的总线接口（如APB, AXI-Lite）或直接寄存器访问实现。

5.  **FIFOs/Buffers:**
    *   **TX FIFO:** 位于用户接口和帧组装逻辑之间，用于缓冲待发送的数据包，吸收上层数据突发。
    *   **RX FIFO:** 位于帧解析逻辑和用户接口之间，用于缓冲接收到的有效帧，吸收上层处理延迟。
    *   选择合适的FIFO深度对性能和避免溢出至关重要。考虑最大帧大小（~1522字节 + 前导/SFD）和链路速率。

#### **关键考虑因素与难点：**

1.  **时序与时钟：**
    *   **125 MHz 时钟域：** GMII/RGMII工作在125MHz。确保你的逻辑满足该频率下的时序收敛。使用流水线设计。
    *   **跨时钟域 (CDC)：** 用户接口时钟 (`user_clk`) 通常与125MHz (`eth_clk`) 不同。MAC地址配置、状态读取、数据包传递都需要进行可靠的CDC处理（FIFO、握手、脉冲同步器）。
    *   **RGMII 时钟/数据偏移：** RGMII接口需要仔细处理时钟和数据/控制信号之间的PCB走线延迟匹配。FPGA内部的IDDR/ODDR和IO约束（如 `set_input_delay`/`set_output_delay`）必须正确设置。

2.  **CRC32 实现：**
    *   需要在发送和接收路径上高效、低延迟地实时计算CRC32。LFSR是最常用的方法。注意位序（LSB first vs MSB first）和多项式约定（IEEE 802.3要求特定形式）。优化实现以匹配125MHz的吞吐量。

3.  **资源消耗：**
    *   FIFO（特别是用于存储完整帧的FIFO）会消耗大量Block RAM (BRAM)。
    *   CRC32计算逻辑。
    *   状态机和控制逻辑。
    *   确保设计在目标FPGA器件的资源范围内。

4.  **PHY 初始化和管理：**
    *   PHY芯片通常需要通过 **MDIO (Management Data Input/Output)** / **MIIM (MII Management)** 接口进行配置（复位、设置工作模式、自协商、读取链路状态和诊断信息）。
    *   需要在Verilog中实现一个简单的MDIO Master控制器（状态机）。

5.  **验证：**
    *   **仿真：** 使用SystemVerilog/UVM或类似方法搭建强大的测试平台（Testbench）。测试用例应覆盖：各种长度帧（最小46B，最大1522B）、错误帧（CRC错、短帧）、广播/组播/单播帧、背压情况、IFG、流控（pause帧）等。
    *   **回环测试：**
        *   **内部回环 (Loopback)：** 将MAC的TX直接连接到MAC的RX（在FPGA内部），绕过PHY。验证基本功能。
        *   **外部回环 (Loopback)：** 通过网线连接FPGA板载PHY和自己的端口，或连接到另一个设备/测试仪。需要PHY支持回环模式。
    *   **使用网络测试仪：** Ixia, Spirent, 或开源工具如 `scapy`/`tcpreplay` 生成流量，使用Wireshark捕获分析。

#### **开发流程建议：**

1.  **明确需求：** 接口类型（RGMII最常见）？需要哪些功能（基本收发、流控、VLAN、时间戳等）？目标FPGA平台？
2.  **选择参考：** 研究Xilinx的Tri-Mode Ethernet MAC (TEMAC) / AXI Ethernet Subsystem 或 Intel (Altera) 的LL Ethernet MAC IP核的文档（即使你不用它们）。开源项目（如Verilog Ethernet）也是很好的学习资源。
3.  **模块化设计：** 清晰划分发送路径、接收路径、接口逻辑、控制逻辑、FIFO。
4.  **自底向上或自顶向下实现：** 从一个关键小模块（如CRC32计算器）开始验证，或者先搭建好顶层结构和接口。
5.  **仿真优先：** 在RTL级进行彻底仿真，覆盖所有关键场景和边界条件。
6.  **约束与综合：** 编写精确的时序约束（`.xdc` 或 `.sdc`），特别是针对RGMII接口。运行综合和布局布线，解决时序违例。
7.  **板级测试：** 下载到FPGA开发板，连接PHY和网络。从简单的回环测试开始，逐步进行实际网络通信测试。使用示波器/逻辑分析仪（特别是对RGMII信号）和软件抓包工具（Wireshark）进行调试。

### 使用RGMII进行千兆以太网传输时的双边沿采样设计要点

在Verilog中实现双边沿采样（即在时钟的上升沿和下降沿都采样数据）时，需要特别注意以下关键问题：

---

#### **1. 综合可行性**
- **标准触发器限制**：FPGA/ASIC中的物理触发器通常只支持**单一时钟边沿**（上升沿或下降沿）。直接在同一个`always`块中使用`@(posedge clk or negedge clk)`会导致综合错误。
- **解决方案**：
  - 使用**两个独立的always块**（一个用`posedge`，一个用`negedge`）。
  - 调用FPGA厂商提供的**专用DDR原语**（如Xilinx的`IDDR`或Intel的`DDIO`）。

---

#### **2. 时序约束**
- **双倍数据速率要求**：数据必须在**半个时钟周期**内满足建立时间（Setup Time）和保持时间（Hold Time）。
  ```verilog
  always @(posedge clk) begin  // 上升沿采样
      data_rise <= din;
  end
  
  always @(negedge clk) begin  // 下降沿采样
      data_fall <= din;
  end
  ```
- **约束挑战**：需对时钟的**两个边沿**分别约束，工具可能难以满足时序。

---

#### **3. 数据对齐**
- **输入数据相位**：数据必须与时钟边沿中心对齐（例如DDR接口中的"眼图中心"）。
- **时钟抖动敏感**：双边沿采样对时钟抖动（Jitter）的容忍度更低。

---

#### **4. 避免功能错误**
- **竞争风险**：若在同一个`always`块中混合双边沿，会导致仿真与综合不匹配：
  ```verilog
  // 错误示例！可能通过仿真但无法综合
  always @(posedge clk or negedge clk) begin
      data <= din; 
  end
  ```
- **正确写法**：分离逻辑到两个块中，并用寄存器暂存结果：
  ```verilog
  reg data_rise, data_fall;
  
  always @(posedge clk) data_rise <= din;
  always @(negedge clk) data_fall <= din;
  
  assign dout = (clk) ? data_rise : data_fall; // 组合逻辑输出
  ```

---

#### **5. 时钟域问题**
- **跨时钟域同步**：双边沿采样本质是**两个时钟域**（上升沿域和下降沿域）。若后续逻辑工作在单边沿，需要同步机制（如FIFO或握手）。

---

#### **6. 使用专用原语（推荐！）**
- **FPGA原语优势**：直接调用厂商提供的DDR触发器，可保证时序、避免设计风险。
  - **Xilinx IDDR**：
    ```verilog
    IDDR #(
      .DDR_CLK_EDGE("OPPOSITE_EDGE") // 模式选择
    ) iddr_inst (
      .Q1(data_rise),  // 上升沿数据
      .Q2(data_fall),  // 下降沿数据
      .C(clk),         // 时钟
      .D(din)          // 输入
    );
    ```
  - **Intel DDIO**：
    ```verilog
    ddio_in ddio_inst (
      .datain    (din),
      .clk       (clk),
      .dataout_h (data_rise), // 上升沿数据
      .dataout_l (data_fall)  // 下降沿数据
    );
    ```

---

#### **7. 仿真与测试**
- **测试平台**：需在仿真中覆盖**时钟两个边沿的数据变化**，验证时序。
- **静态时序分析（STA）**：必须针对上升沿和下降沿分别检查路径。

---

#### **总结：最佳实践**
1. **避免直接编码双边沿触发器**，除非使用厂商原语。
2. **分离为两个单边沿`always`块**并严格约束时序。
3. **优先使用FPGA的DDR原语**（如`IDDR`/`DDIO`），确保可靠性和性能。
4. **详细注释设计**，明确双边沿采样的意图和风险。

> ⚠️ 注意：双边沿采样通常用于高速接口（如DDR内存、千兆以太网），普通逻辑设计应避免使用，优先考虑单边沿设计以降低复杂度。

### 双边沿采样时序约束要点

当分离为两个单边沿`always`块实现双边沿采样时，严格的时序约束至关重要。以下是完整的约束方法和实践指南：

#### 时序约束的核心挑战

| 约束类型     | 上升沿路径   | 下降沿路径       | 关键差异             |
| ------------ | ------------ | ---------------- | -------------------- |
| 建立时间     | 整个时钟周期 | **半个时钟周期** | 下降沿路径要求更严格 |
| 保持时间     | 整个时钟周期 | **半个时钟周期** | 下降沿路径要求更严格 |
| 数据有效窗口 | 较宽         | **很窄**         | 下降沿路径容错性低   |

#### 完整约束方法（Vivado示例）

##### 1. 基础时钟定义
```tcl
# 定义主时钟（假设100MHz，周期10ns）
create_clock -name sys_clk -period 10.000 [get_ports clk]
```

##### 2. 输入延迟约束（关键！）
```tcl
# 设置输入端口约束（din为输入数据端口）
set_input_delay -clock sys_clk -max 3.000 [get_ports din]  # 最大延迟
set_input_delay -clock sys_clk -min 1.000 [get_ports din]  # 最小延迟
```

##### 3. 专用下降沿路径约束
```tcl
# 创建虚拟时钟处理下降沿路径
create_clock -name sys_clk_fall -period 10.000 -waveform {5 10} [get_ports clk]

# 对下降沿寄存器设置特定约束
set_input_delay -clock sys_clk_fall -max 1.500 [get_ports din]  # 更严格的最大延迟
set_input_delay -clock sys_clk_fall -min 0.500 [get_ports din]  # 更严格的最小延迟
```

##### 4. 多周期路径设置
```tcl
# 告诉工具下降沿路径只有半个周期的时间
set_multicycle_path -setup -end -from [get_clocks sys_clk] -to [get_clocks sys_clk_fall] 1
set_multicycle_path -hold -end -from [get_clocks sys_clk] -to [get_clocks sys_clk_fall] 0
```

##### 5. 输出约束（如有输出）
```tcl
set_output_delay -clock sys_clk -max 4.000 [get_ports dout]
set_output_delay -clock sys_clk -min 0.500 [get_ports dout]
```

#### 完整Verilog示例代码

```verilog
module dual_edge_sampler (
    input  wire clk,    // 系统时钟
    input  wire rst_n,  // 复位（低有效）
    input  wire din,    // 输入数据
    output wire dout    // 输出数据
);

// 上升沿采样寄存器
reg data_rise;
always @(posedge clk or negedge rst_n) begin
    if (!rst_n) 
        data_rise <= 1'b0;
    else 
        data_rise <= din;
end

// 下降沿采样寄存器
reg data_fall;
always @(negedge clk or negedge rst_n) begin
    if (!rst_n) 
        data_fall <= 1'b0;
    else 
        data_fall <= din;
end

// 数据选择器（根据当前时钟电平输出）
assign dout = clk ? data_rise : data_fall;

endmodule
```

#### 时序约束要点详解

##### 1. 建立时间约束（Setup Time）
- **下降沿路径**只有**半个时钟周期**满足建立时间
- 100MHz时钟示例：
  - 上升沿路径：10ns时间窗口
  - 下降沿路径：仅5ns时间窗口
- 约束策略：
  ```tcl
  set_max_delay -from [get_pins din] -to [get_pins data_fall_reg/D] 5.000 -datapath_only
  ```

##### 2. 保持时间约束（Hold Time）
- 下降沿路径的保持时间要求更严格
- 约束策略：
  ```tcl
  set_min_delay -from [get_pins din] -to [get_pins data_fall_reg/D] 0.200 -datapath_only
  ```

##### 3. 时钟不确定性设置
```tcl
# 增加时钟抖动约束
set_clock_uncertainty -setup 0.150 [get_clocks sys_clk]
set_clock_uncertainty -hold 0.100 [get_clocks sys_clk]

# 对下降沿路径使用更严格的约束
set_clock_uncertainty -setup 0.100 [get_clocks sys_clk_fall]
set_clock_uncertainty -hold 0.075 [get_clocks sys_clk_fall]
```

#### 最佳实践与调试技巧

1. **专用时钟约束组**
   ```tcl
   group_path -name rise_path -from [get_clocks sys_clk]
   group_path -name fall_path -from [get_clocks sys_clk_fall] -critical_range 0.5
   ```

2. **时序例外报告**
   ```tcl
   report_timing -setup -fall_from [get_clocks sys_clk] -to [get_cells data_fall_reg*]
   report_timing -hold -rise_from [get_clocks sys_clk] -to [get_cells data_fall_reg*]
   ```

3. **物理布局约束**
   ```tcl
   # 确保上升沿和下降沿触发器物理位置靠近
   set_property PACKAGE_PIN F5 [get_ports din]
   set_property IOSTANDARD LVCMOS33 [get_ports din]
   ```

4. **时序裕量检查**
   - 确保下降沿路径有至少0.5ns的正裕量
   - 特别关注高温/低压条件下的时序

#### 替代方案：使用厂商原语（推荐）

```verilog
// Xilinx IDDR原语示例
IDDR #(
    .DDR_CLK_EDGE("OPPOSITE_EDGE"),
    .INIT_Q1(1'b0),
    .INIT_Q2(1'b0),
    .SRTYPE("SYNC")
) iddr_inst (
    .Q1(data_rise),  // 上升沿数据
    .Q2(data_fall),  // 下降沿数据
    .C(clk),         // 时钟
    .CE(1'b1),       // 时钟使能
    .D(din),         // 输入数据
    .R(1'b0),        // 复位
    .S(1'b0)         // 置位
);
```

**使用原语的优势：**
1. 厂商已预定义所有时序约束
2. 专用硬件路径保证性能
3. 避免手动约束错误
4. 支持更高速率（DDR3/DDR4等）

#### 总结：双边沿采样约束要点

1. **分离约束**：对上升沿和下降沿路径分别约束
2. **严格限制**：下降沿路径按半个周期约束
3. **输入延迟**：设置精确的max/min输入延迟
4. **时钟建模**：使用虚拟时钟或时钟组
5. **时序例外**：正确设置多周期路径
6. **物理实现**：确保相关元件布局靠近
7. **厂商原语**：优先使用IDDR/DDIO等专用元件

> 📌 **关键提示**：在100MHz以上设计中，强烈建议使用FPGA厂商提供的专用DDR原语，它们经过硅验证且包含预定义的时序约束，可显著降低设计风险。

# 四通道三自由度FPGA程序

## 程序结构

1. 31阶FIR滤波器
2. 寻找最值和平均值
3. 直流偏置矫正+不等幅矫正(寻找最值并交叉相乘)
4. 非正交矫正(相加相减)(未来可用最小二乘矫正)
5. 不等幅矫正
6. cordic计算两路之间的角度，即相位
7. 相位解缠
8. 相位进FIFO
9. 串口低速读取FIFO中的数据并发送
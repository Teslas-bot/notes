# How to verify ?

![image-20250708210153598](SystemVerilog_for_Verification.assets/image-20250708210153598.png)

# Why System Verilog for Verification?

![image-20250708210309285](SystemVerilog_for_Verification.assets/image-20250708210309285.png)

# System Verilog Features

![image-20250708210410156](SystemVerilog_for_Verification.assets/image-20250708210410156.png)

# Basic types of System Verilog

[数据类型 | EasyFormal](https://easyformal.com/systemverilog/01.data-types/)

## Logic

* **logic** replaces **reg** of Verilog
* reg keyword gets confused with filpflop
  * user was not able to understand whether reg will derectly mapped with filp-flop, latch, or any other thing
  * But in System Verilog, user doesn't need to worry about that
* logic can be net or reg depending on usage
* logic is a 4 state data type

| 4-State value |               Represents               | Equivalent 2-State value |
| :-----------: | :------------------------------------: | :----------------------: |
|       0       |    logic zero or a false condition     |            0             |
|       1       |     logic one or a true condition      |            1             |
|       X       |    unknown logic value (don't care)    |            0             |
|       Z       | high-impedance state (open connection) |            0             |

**The advantage of having logic as data type is there is no need of port list rules.**

[SystemVerilog logic、wire、reg数据类型详解 - 知乎](https://zhuanlan.zhihu.com/p/38563777)

**SystemVerilog的logic类型**

SystemVerilog在Verilog基础上新增支持**logic**数据类型，**logic**是**reg**类型的改进，它既可被过程赋值也能被连续赋值，编译器可自动推断**logic**是**reg**还是**wire**。唯一的限制是**logic**只允许一个输入，不能被多重驱动，所以**inout**类型端口不能定义为**logic**。不过这个限制也带来了一个好处，由于大部分电路结构本就是单驱动，如果误接了多个驱动，使用**logic**在编译时会报错，帮助发现bug。所以单驱动时用**logic**，多驱动时用**wire**。

在[Jason的博客](https://link.zhihu.com/?target=http%3A//www.verilogpro.com/verilog-reg-verilog-wire-systemverilog-logic)评论中，Evan还提到一点**logic**和**wire**的区别。**wire**定义时赋值是连续赋值，而**logic**定义时赋值只是赋初值，并且赋初值是不能被综合的。

```verilog
wire mysignal0 = A & B;     // continuous assignment, AND gate
logic mysignal1 = A & B;    // not synthesizable, initializes mysignal1 to the value of A & B at time 0 and then makes no further changes to it.
logic mysignal2;
assign mysignal2 = A & B;   // Continuous assignment, AND gate
```

## Data Type Classification

![image-20250709094413383](SystemVerilog_for_Verification.assets/image-20250709094413383.png)

## Groups of Data Object

![image-20250709094844390](SystemVerilog_for_Verification.assets/image-20250709094844390.png)

## Net

![image-20250709100650077](SystemVerilog_for_Verification.assets/image-20250709100650077.png)

个人理解，wire理解为导线，tri理解为三态导线，uwire理解为未连接的导线（只允许有一个驱动）。wor, trior分别是或门，三态或门；wand, triand分别是与门，三态与门。

multiple drivers多个驱动的意思是，对net类型的数据类型的数据进行多个逻辑驱动。例如：

```verilog
module abc ();
    wire a;
    wor b;
    wand c;
    tri data;
    logic bus0, bus1, s0, s1;
    
    // multiple drivers of a 
    assign a = bus0;
    assign a = bus1;
    
    // multiple drivers of b
    assign b = b0;
    assign b = b1;
    
    // multiple drivers of c
    assign c = b0;
    assign c = b1;
    
    // multiple drivers of data
    assign data = s0 ? bus0 : 1'bz;
    assign data = s1 ? bus0 : 1'bz;
    
    initial begin
        bus0 = 1'b1;
        bus1 = 1'b1;
        s0 = 1'b1;
        s1 = 1'b1;
        b0 = 1'b1;
        b1 = 1'b0;
        #1 $display{"a = %b, data = %b, b = %b, c = %b", a , data, b, c};
    end

endmodule
```

上述仿真文件的结果为

```shell
a = x, data = x, b = 1; c = 0;
```

根据仿真结果可知，当net类型出现multiple drivers的情况时，会按照上图的真值表进行输出。

![image-20250709202033459](SystemVerilog_for_Verification.assets/image-20250709202033459.png)

在 SystemVerilog 中，**net 类型**（Net Types）用于建模物理信号线的行为，它们的值由驱动源决定（不能直接赋值，需通过连续赋值或模块端口驱动）。SystemVerilog 提供了多种 net 类型，每种类型对应不同的硬件行为和驱动冲突解决规则。以下是所有 **net 类型的详解**。

---

### **1. 基本 Net 类型**
#### **1.1 `wire`**
- **行为**：最常用的 net 类型，表示物理导线。
- **驱动冲突**：多个驱动源冲突时，结果为 `x`（未知态）。
- **默认值**：未驱动时为 `z`（高阻态）。
- **用途**：普通信号连接。
- **示例**：
  ```systemverilog
  wire a;
  assign a = b & c; // 通过连续赋值驱动
  ```

#### **1.2 `tri`**
- **行为**：与 `wire` 完全相同，仅用于提高代码可读性（表示三态信号）。
- **驱动冲突**：同 `wire`。
- **用途**：建模三态总线（但需配合三态驱动器使用）。
- **示例**：
  ```systemverilog
  tri [7:0] data_bus;
  assign data_bus = enable ? data : 'z;
  ```

---

### **2. 特殊驱动规则的 Net 类型**
#### **2.1 `wand`（Wired-AND）**
- **行为**：线与逻辑（所有驱动必须为 `1`，否则结果为 `0`）。
- **驱动冲突**：多个驱动源按逻辑与合并。
- **用途**：开漏输出（如 I²C 总线）。
- **示例**：
  
  ```systemverilog
  wand sda;
  assign sda = (enable1) ? 1'b0 : 1'bz; // 设备 1 驱动
  assign sda = (enable2) ? 1'b0 : 1'bz; // 设备 2 驱动
  ```

#### **2.2 `triand`**

- **行为**：与 `tri` 类似，但驱动冲突时按线与逻辑合并。

- **用途**：建模多驱动线或总线（类似 `wand`，但更明确三态特性）。

- **示例**：

  ```systemverilog
  trior [3:0] bus;
  assign bus = (drv1) ? 4'hF : 'z;
  assign bus = (drv2) ? 4'h3 : 'z; // 结果为 4'hF and 4'h3 = 4'h3
  ```

#### **2.3 `wor`（Wired-OR）**

- **行为**：线或逻辑（所有驱动必须为 `0`，否则结果为 `1`）。
- **驱动冲突**：多个驱动源按逻辑或合并。
- **用途**：线或总线（如中断信号）。
- **示例**：
  ```systemverilog
  wor interrupt;
  assign interrupt = (irq1) ? 1'b1 : 1'bz;
  assign interrupt = (irq2) ? 1'b1 : 1'bz;
  ```

#### **2.4 `trior`**
- **行为**：与 `tri` 类似，但驱动冲突时按线或逻辑合并。
- **用途**：建模多驱动线或总线（类似 `wor`，但更明确三态特性）。
- **示例**：
  
  ```systemverilog
  trior [3:0] bus;
  assign bus = (drv1) ? 4'hF : 'z;
  assign bus = (drv2) ? 4'h3 : 'z; // 结果为 4'hF | 4'h3 = 4'hF
  ```

---

### **3. 保持特性的 Net 类型**
#### **3.1 `trireg`**
- **行为**：当无驱动时，保持最后一次驱动的值（模拟电容特性）。
- **驱动冲突**：多个驱动源冲突时，结果为 `x`。
- **用途**：三态总线保持、模拟硬件电容效应。
- **示例**：
  ```systemverilog
  trireg [7:0] hold_bus;
  assign hold_bus = enable ? data : 'z; // 断开后保持 data 的值
  ```

---

### **4. 电源和地 Net 类型**
#### **4.1 `supply0`**
- **行为**：固定为逻辑 `0`（地）。
- **用途**：建模全局地信号。
- **示例**：
  ```systemverilog
  supply0 vss;
  ```

#### **4.2 `supply1`**
- **行为**：固定为逻辑 `1`（电源）。
- **用途**：建模全局电源信号。
- **示例**：
  ```systemverilog
  supply1 vdd;
  ```

---

### **5. 其他 Net 类型（组合逻辑）**
#### **5.1 `tri0`**
- **行为**：未驱动时默认为 `0`，驱动冲突时按 `wire` 规则处理。
- **用途**：模拟有下拉电阻的信号线。
- **示例**：
  ```systemverilog
  tri0 with_pull0;
  assign with_pull0 = (drv) ? 1'b1 : 'z; // 未驱动时为 0
  ```

#### **5.2 `tri1`**
- **行为**：未驱动时默认为 `1`，驱动冲突时按 `wire` 规则处理。
- **用途**：模拟有上拉电阻的信号线。
- **示例**：
  ```systemverilog
  tri1 with_pull1;
  assign with_pull1 = (drv) ? 1'b0 : 'z; // 未驱动时为 1
  ```

#### **5.3 `triz`**
- **行为**：与 `tri` 相同，仅用于提高代码可读性。
- **用途**：显式表示高阻态驱动。

#### **5.4 `uwire`（Unresolved Wire）**
- **行为**：不允许多个驱动源，否则报错。
- **用途**：确保信号线只有一个驱动源（提高设计安全性）。
- **示例**：
  ```systemverilog
  uwire single_drv;
  assign single_drv = a & b; // 必须唯一驱动
  ```

---

### **6. Net 类型对比表**
| Net 类型  | 初始值 | 无驱动时值 | 驱动冲突规则      | 可综合性 | 典型用途           |
| --------- | ------ | ---------- | ----------------- | -------- | ------------------ |
| `wire`    | `z`    | `z`        | 多驱动 → `x`      | ✔️        | 普通信号连接       |
| `tri`     | `z`    | `z`        | 同 `wire`         | ✔️        | 三态总线           |
| `wand`    | `z`    | `z`        | 线与（0 > z > 1） | ✔️        | 开漏总线（I²C）    |
| `wor`     | `z`    | `z`        | 线或（1 > z > 0） | ✔️        | 中断信号           |
| `trior`   | `z`    | `z`        | 线或              | ✖️        | 多驱动线或总线     |
| `triand`  | `z`    | `z`        | 线与              | ✔️(部分)  | 三态线与总线       |
| `trireg`  | `x`    | 保持最后值 | 多驱动 → `x`      | ✖️        | 电容保持、三态总线 |
| `supply0` | `0`    | `0`        | 固定值            | ✔️        | 地信号             |
| `supply1` | `1`    | `1`        | 固定值            | ✔️        | 电源信号           |
| `tri0`    | `0`    | `0`        | 多驱动 → `wire`   | ✔️        | 下拉电阻模拟       |
| `tri1`    | `1`    | `1`        | 多驱动 → `wire`   | ✔️        | 上拉电阻模拟       |
| `uwire`   | `z`    | `z`        | 不允许多驱动      | ✔️        | 单驱动信号线       |

---

### **7. 使用注意事项**
1. **可综合性**：
   - `trireg`、`trior` 等不可综合（仅用于仿真）。
   - `wire`、`tri`、`wand`、`wor` 等可综合（需符合综合工具支持）。

2. **驱动优先级**：
   
- `wand` 和 `wor` 的冲突解决规则依赖信号强度（如 `0` > `z` > `1`）。
   
3. **初始化**：
   - `trireg` 可通过 `initial` 块初始化：
     ```systemverilog
     initial begin
       r = 1'b1; // 初始化 trireg
     end
     ```

4. **避免混淆**：
   
   - `wire` 和 `reg` 是两种不同类型：`wire` 是 net 类型，`reg` 是变量类型（用于过程赋值）。

---

### **8. 总结**
SystemVerilog 的 net 类型覆盖了从简单信号线到复杂硬件行为的建模需求：
- **基础类型**：`wire`、`tri`。
- **特殊逻辑**：`wand`（线与）、`wor`（线或）。
- **保持特性**：`trireg`（电容保持）。
- **电源/地**：`supply0`、`supply1`。
- **安全设计**：`uwire`（单驱动检查）。

选择合适的 net 类型需根据设计需求（如三态、线与、保持特性）和综合工具的支持情况。在实际设计中，`wire` 是最常用的类型，而 `trireg` 和 `wand` 多用于仿真和验证场景。

## Variable
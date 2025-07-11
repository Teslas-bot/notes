# 华为2024FPGA工程师面试题

Q: FPGA的内部组成？

A: 可编程逻辑单元（Configurable Logic Blocks，CLB）、可编程互连资源（Programmable Interconnect Resources，PIR）和输入/输出资源（I/O Blocks，IOBs）。可编程逻辑单元（CLB）是FPGA最基本的计算单元，用于实现各种数字电路功能。每个CLB包含多个LUT（Lookup Table），寄存器，以及一些MUX、ALU、加法器等，可以进行任意的布尔运算、寄存器存储等操作。 可编程互连资源（PIR）是FPGA中实现信号传输的主要资源，包括可编程连接点、交叉开关、线缆等，可以将各个CLB中的逻辑单元连接起来，实现任意的数字电路连接。 输入/输出资源（IOBs）用于与外部设备进行数据交互，包括输入/输出端口、时钟管理器、数据缓存器、电压电平转换器等。IOBs可以实现与外部设备的数据通信，同时还可以实现时钟分频、时钟缓存等功能。

Q: 查找表与触发器是怎么构成分布式RAM的？
**解题思路**
查找表（Lookup Table，简称LUT）和触发器（Flip-Flop）是构成分布式RAM的基本元素。具体实现方式如下： 首先，将输入地址分为两部分，高位地址和低位地址。高位地址通过解码器选择要访问的RAM块，低位地址用于选择RAM块中的行。 然后，将选择的RAM块中的每一行都表示为一个查找表，每个查找表包含N位输入和M位输出。查找表通过使用输入地址的低位地址来确定要选择的行，然后将输入地址的高位地址作为查找表的输入，得到查找表的输出。 最后，将查找表的输出连接到触发器的输入，触发器用于存储查找表的输出数据。这样，每个RAM块中的查找表和触发器组合在一起形成了分布式RAM。这种设计可以提高RAM访问速度和减少功耗。
**详解**

**核心概念：**

- **分布式RAM：** 这是在FPGA（现场可编程门阵列）中实现RAM的一种方式。它**直接利用FPGA逻辑块（CLB - Configurable Logic Block）中的查找表（LUT）资源**来构建小型、快速、分散在整个FPGA架构中的存储器，而不是使用专用的、大型的Block RAM（BRAM）模块。
- **查找表（LUT）：** 这是FPGA逻辑单元的基本构建块。一个N输入的LUT本质上是一个微小的、可配置的 `2^N x 1` 位SRAM（静态随机存取存储器）。它存储了 `2^N` 个位（0或1），每个位对应一个唯一的N位输入组合。当给定一个N位地址输入时，LUT会输出存储在该地址位置上的位值。
- **触发器（FF）：** 这是FPGA逻辑单元中的基本存储元件，用于存储1位数据。它在时钟边沿（通常是上升沿）捕获其输入（D）的值，并在输出（Q）保持该值，直到下一个时钟边沿。

**构建分布式RAM的详细过程：**

1. **将地址总线拆分为高位和低位：**

   - 假设我们要构建一个容量为 `Depth x Width` 位的分布式RAM（例如，64x4位）。
   - 地址总线宽度 `Addr_Width = log2(Depth)`（例如，64深度需要6位地址 `A[5:0]`）。
   - **关键步骤：** 将这 `Addr_Width` 位地址分为两部分：
     - **高位地址 (`A_high`)：** 用于选择哪个逻辑块（或者说哪一组LUT）包含目标数据。高位地址的位数决定了需要多少个独立的LUT块。位数 `= log2(Number_of_LUT_Blocks)`。
     - **低位地址 (`A_low`)：** 用于在每个被选中的LUT块内部进行寻址。低位地址的位数 `= log2(LUT_Depth)`，其中 `LUT_Depth` 通常是 `2^N`（N是LUT的输入数，常见为4、5或6）。

   **示例 (64x4 RAM)：**

   - 深度 = 64 -> `Addr_Width = 6` (`A[5:0]`)。
   - 假设使用4输入LUT（LUT4，可存储16位）。
   - 要存储64个位置，需要 `64 / 16 = 4` 个LUT块。
   - 因此，将地址 `A[5:0]` 拆分：
     - **高位地址 `A_high = A[5:4]` (2位)：** 用于选择4个LUT块中的1个 (`00`, `01`, `10`, `11`)。
     - **低位地址 `A_low = A[3:0]` (4位)：** 用于在选中的LUT块内部的16个位置中选择1个。

2. **高位地址解码与LUT块选择：**

   - 高位地址 `A_high` 被送入一个**解码器（Decoder）**。
   - 解码器有 `2^(位数(A_high))` 个输出线（在我们的例子中是4条线：`Sel0`, `Sel1`, `Sel2`, `Sel3`）。
   - 在任何时候，只有一条选择线（根据 `A_high` 的值）被激活（通常为高电平），其余为低电平。这条激活的选择线**指明了当前访问请求（读或写）应该作用于哪个LUT块**。

3. **LUT作为存储单元：**

   - 每个LUT块由多个LUT组成，存储RAM的**一位宽**数据。RAM的位宽 `Width` 决定了每个LUT块需要多少个LUT。
   - **关键点：** 分布式RAM的每一位（bit）由**一个独立的LUT**存储。
   - **示例 (64x4 RAM)：**
     - 位宽 = 4位。
     - 需要4个LUT块（由高位地址选择）。
     - **每个LUT块包含4个LUT4。**
     - 在LUT块0中：
       - `LUT0_Block0` 存储所有64个地址位置上的**第0位**数据。
       - `LUT1_Block0` 存储所有64个地址位置上的**第1位**数据。
       - `LUT2_Block0` 存储所有64个地址位置上的**第2位**数据。
       - `LUT3_Block0` 存储所有64个地址位置上的**第3位**数据。
     - 其他LUT块（1, 2, 3）的结构完全相同，分别存储各自地址段（`A[5:4]=01`, `10`, `11`）对应的64位数据中的4位（每个位一个LUT）。
   - **寻址：** 对于读操作或写操作，**同一个LUT块内的所有LUT** 都接收相同的低位地址 `A_low`。这个地址告诉每个LUT要访问其内部存储的16个位中的哪一个。
   - **配置：** LUT在配置时被编程为特定的真值表，其内容就是它负责存储的RAM数据位。

4. **写操作：**

   - 写操作需要时钟（`clk`）和写使能（`we`）信号。
   - 写数据总线 `Data_in[Width-1:0]` 被广播到所有LUT块的对应输入上。
   - **关键步骤：**
     - 高位地址 `A_high` 经过解码器产生选择信号 `SelX`。
     - **只有当 `we` 有效（例如高电平）并且 `SelX` 有效时，对应的第X个LUT块才被“使能”进行写入。**
     - 在时钟 `clk` 的上升沿（或其他指定边沿），**被使能的LUT块内的每一个LUT** 会根据当前的低位地址 `A_low`，将其对应的输入数据线（`Data_in[0]` 写入 `LUT0_BlockX`，`Data_in[1]` 写入 `LUT1_BlockX`，等等）的值**写入**到其内部由 `A_low` 指定的存储位置。
     - 其他未被 `SelX` 选中的LUT块忽略写操作，其内容保持不变。

5. **读操作：**

   - 读操作可以是**异步**（组合逻辑，无时钟）或**同步**（有时钟）。
   - **异步读：**
     - 给定地址 `A[Addr_Width-1:0]`。
     - 高位地址 `A_high` 解码选择激活的LUT块（`SelX`）。
     - 低位地址 `A_low` 送到所有LUT块的所有LUT。
     - **关键点：** 只有**被 `SelX` 选中的LUT块内的LUT** 会根据 `A_low` **立即输出**其存储的值。
     - 未被选中的LUT块输出未定义（通常是0或上次选中的值，取决于实现，但设计上应忽略）。
     - 被选中的LUT块内每个LUT的输出（`LUTY_BlockX_out`）直接组合成该地址的读出数据 `Data_out[Y]`。
   - **同步读：**
     - 这是你解题思路中提到的“将查找表的输出连接到触发器的输入”的应用场景。
     - 异步读路径（如上述）仍然存在：LUT根据地址输出存储的值。
     - **关键步骤：** 在选中的LUT块的输出端（即每个LUT的输出后面），连接一个**触发器（FF）**。
     - 当读地址变化时，LUT输出会立即（异步地）变化。
     - 在时钟 `clk` 的上升沿（或其他指定边沿），这些LUT的输出值会被捕获到它们各自对应的触发器中。
     - 触发器的输出（`Q`）才作为稳定的、同步的读数据 `Data_out[Width-1:0]` 输出。
     - **作用：** 同步读通过触发器实现了**输出寄存器**。这带来了两个主要好处：
       1. **改善时序：** 将组合逻辑路径（地址->LUT输出）与下游电路隔离开，使得时序分析更简单，更容易满足时钟约束，达到更高频率。
       2. **消除毛刺：** 地址变化在LUT内部传播时可能产生短暂的毛刺，触发器捕获的是时钟边沿瞬间稳定的值，避免了毛刺传播到下游逻辑。
# Efinity Timing Closure User Guide(时钟收敛指南)

本笔记是参考Efinity官网的时钟收敛指南（下称之指南）进行制作。笔记目录与指南目录保持一致。

常见时钟术语中英文对照

| 中文术语 | 英文术语           |
| -------- | ------------------ |
| 时钟延迟 | clock latency      |
| 时钟偏移 | clock skew         |
| 时钟抖动 | clock jitter       |
| 时钟频率 | clock frequency    |
| 主时钟   | master clock       |
| 从时钟   | slave clock        |
| 同步时钟 | synchronous clock  |
| 异步时钟 | asynchronous clock |
| 时钟域   | clock domain       |

## Constraining Clocks (时钟约束)

当编译一个SDC文件(efinity的时钟约束文件)时，首要的任务时定义Verilog设计中的时钟和它们的关系。你应该设置约束来定义时钟和它们之间的关系。然后，你可以根据需要针对每个时钟限制其IO管脚。这章随后的小节解释了定义时钟及其关系背后的理论。

### Defining Clocks (定义时钟)

时钟源可以来自于 interface blocks，比如PLL或是晶振；或者也可以通过GPIO引脚来源于你的电路板。你应该使用`create_clock`和`create_generated_clock`这两个约束语句来定义和识别时钟。

---

**Example: Define a Clock**

This constraint creates a clock, clk1, with a period of 10ns:

```sdc
create_clock -period 10 -name clk1 [get_ports clk1]
```

---

**Example: Define a Clock with a Wave form**

This example defines a clock with a 10 ns period and 50/50 duty cycle, but the first rising clock edge is phase shifted 25% to start at 2.5ns.

```sdc
create_clock -period 10.00 -waveform {2.50 7.50} -name clk1 [get_ports clk1]
```

---

`create_generated_clock`约束定义了内部生成的时钟(如门控时钟)与其源时钟之间的关系。此约束仅支持`divide_by`, `multiply_by`, `duty_cycle`, `inverted`选项。

---

**Example: Creating Clocks**

这个例子显示了基本时钟`clk`和内部生成时钟`clkdiv2`的约束。

![image-20251105112544698](efinity时序收敛指南.assets/image-20251105112544698.png)

```sdc
create_clock -name clk -period 10 [get_ports clk]
create_generated_clock -source clk -divide_by 2 clkdiv2
```

---

Virtual clocks (虚拟时钟) 是不分配到时钟节点的时钟。虚拟时钟用于表示off-chip clocks (不连接到FPGA内部的时钟)。使用`set_input_delay`和`set_output_delay`来约束虚拟时钟。

#### Using the `create_clock` Constraint

手册中这部分详述了Efinity软件的interface的任意接口都可作为一个时钟源(PLL, GPIOs, MIPI RX Lane, MIPI RX/TX PHY, and JTAG)。并举例说明了Interface Designer 自动生成的 \<*project*\>**.pt.sdc**中，对于不同的时钟源自动生成的约束的区别。可以作为参考。

#### Using the `create_generated_clock` Constraint

Interface Designer 并不会对generated clocks (内部生成的时钟)创建 SDC 约束。通常，设计者会在内核中使用Verilog代码对时钟进行分频，这种分频后的时钟就属于 generated clock 的一种。设计者需要对这些时钟添加约束。

![image-20251105171204643](efinity时序收敛指南.assets/image-20251105171204643.png)

---

**SDC Commands**

```sdc
create_clock -period 10 -name clk0 [get_ports clkin]
create_generated_clock -source [get_ports clkin] -divide_by 2 [get_pins divclk|Q] -name gen_clk0
```

---

#### Virtual Clocks

虚拟时钟用于建模电路板上片外(未接入FPGA)的时钟源。由于FPGA使用（输入或输出）了与该时钟源同步的数据，但未使用（输入或输出）此时钟，故需要对该时钟在FPGA内部建模，这种模型即是虚拟时钟。在你的SDC文件中，你应该使用一个虚拟时钟作为输入输出延迟的参考时钟来替代电路板上的时钟。虚拟时钟提供了一个干净的接口时钟，意味着你不必担心板上的波形偏移。此外，虚拟时钟可以防止时序分析使用过于严格和不切合实际的要求来处理I/O路径。

下图展示了一个使用`set_input_delay`命令约束的虚拟时钟。晶振驱动了时钟焊盘`clk_in`和一个额外的片外的D触发器。从晶振到core上的`clk_in`焊盘的路径是通过interface的。Interface Designer 可以对这个路径添加额外的时钟延迟和时钟不确定性。为了对`data_in`焊盘去除所有额外的时钟延迟和时钟不确定性，你需要使用一个虚拟时钟。

![image-20251105172630591](efinity时序收敛指南.assets/image-20251105172630591.png)

---

**SCD Commands**

```sdc
create_clock -period 40 -name clk_in [get_ports clk_in]
create_clock -period 40 -name virtual_clk
set_input_delay -clock virtual_clk -max 0.3 [get_ports data_in]
set_input_delay -clock virtual_clk _min 0.1 [get_porst data_in]
```

---

请注意，虚拟时钟具有与`clk_in`相同的周期和特征，但它没有一个引用 netlist (网表) 中 net (网络)、port (端口) 或 pin (引脚)的 clock target (时钟目标)。Efinity 软件会为虚拟时钟显示一个的信息消息。

下图展示了如何使用一个通过`set_output_delay`命令约束的虚拟时钟。

![image-20251105173500382](efinity时序收敛指南.assets/image-20251105173500382.png)

---

**SDC Commands**

```sdc
create_clock -period 40 -name clk_in [get_ports clk_in]
creter_clock -period 40 -name virtual_clk
set_output_delay -clock virtual_clk -max 0.4 [get_ports data_out]
set_output_delay -clock virtual_clk -min 0.3 [get_ports data_out]
```

---

---

**Note: **在你的SDC文件中，将virtual clock (虚拟时钟)和 core clock (核心时钟)放在同一个 clock group (时钟组)中，以保证他们是 related (相关的)。In your SDC file, put the virtual clock and core clock in the same clock group so they are related.The software can then analyze the transfers from `virtual_clk` to/from `clk_in`.

---



### Clock Latency (时钟延迟)

源时钟延迟表示从板上时钟源到FPGA中的全局时钟树所需的时间。这个延迟包括：电路板延迟、缓冲器延迟和任何的PLL延迟（包括PLL补偿延迟，该延迟为负）。

大多数情况下你不需要使用`set_clock_latency`。不过，当您想要将外部信号限制到内核寄存器以捕获传输到FPGA的时钟信号的延迟效应时，这是必须的。

你需要基于GPIO延迟，PLL延迟和所有的电路板延迟来计算此延迟。

#### GPIO Clock Latency

#### PLL Local Feedback Clock Latency

#### PLL Core Feedback Clock Latency

#### PLL External Feedback Clock Latency

### Clock Relationships (时钟关系)

默认情况下，Efinity® 软件假定所有时钟都是相关的，它会分析所有时钟域之间的时序并优化所有可能的路径。

如果为两个时钟设置约束，并且不切断它们之间的路径，则软件会尝试在它们之间找到最严格的时钟到时钟延迟要求。如果定时器在 1,000 个时钟周期后找不到两个时钟的公共时钟周期，则确定它们 *non_expandable* (不可扩展)。定时器为这些时钟提供 0.01 ns 的默认约束。如果要覆盖此默认值，请使用`set_max_dela`或`set_min_delay`约束。

#### Setting Constraints for Unrelated Clocks

第一步是分析您的设计，以确定哪些时钟是相关的，哪些不是。然后，您可以使用以下约束其中之一：

* `set_clock_groups` —— 当您想要指定时钟之间的双向约束时使用。通常，这是最简单的方法，也是 Efinity® 定时器分析速度最快的方法。(See `set_clock_groups Constraint`.)
* `set_false_path` —— 当您想要具体说明哪些时钟与哪些端点连接时使用。此约束是单向的，因此您需要指定两个约束，每个方向一个。(See `set_false_path Constraint`.)通常，当您想要指示其中一个时钟域中时序端点子集的 timing exceptings (时序例外)时，可以使用这些约束。

#### Using the set_clock_groups Constraint

使用此约束来定义时钟和您定义的生成时钟之间的关系。通常，只有来自同一源的时钟才相互关联。例如，来自同一PLL的时钟输出或来自单个时钟引脚的时钟输出。任何其他时钟都应指定为不相关。

Unrelated clock groups can be exclusive or asynchronous.

* Exclusive clock groups do not operate at the same time as each other.
* Asynchronous clock groups have no timing relationship between them, for example, clocks driven from two independent PLLs.

使用 `-exclusive` 或 `-asynchronous` 参数选项来定义如何对待时钟组。Efinity® 软件对待两种选项的方式是相同的，但是一些第三方EDA工具使用上述两种约束参数来检查跨时钟域的逻辑是否正确。因此最好在参数约束时根据时钟的关系选择正确的约束参数。

为了说明如何使用`set_clock_groups`设置约束，请考虑具有四个时钟（clk1、clk2、clk3 和 clk4）的设计。设计分析后，确定 clk1 和 clk2 彼此相关，而 clk3 和 clk4 与所有其他 clk4 无关。有两种使用`set_clock_groups`约束的方法，这两种方法都是正确的。

---

**Example: Use a Single Constraint**

The first method is to define the clocks and groups with a single constraint:

```sdc
set_clock_groups -exclusive -group {clk1 clk2} -group {clk3} -group {clk4}
```

---

此约束定义了时钟 clk1、clk2、clk3 和 clk4 之间的关系。如果稍后添加一个额外的时钟 clk5，并且不更新约束，则软件会假定 clk5 与所有其他时钟同步。

---

**Example: Use Separate Constraints**

The second method is to use separate constraints for each group:

```sdc
set_clock_groups -exclusive -group {clk1 clk2}
set_clock_groups -exclusive -group {clk3}
set_clock_groups -exclusive -group {clk4}
```

---

在这种情况下，每个set_clock_groups约束仅指定一个组，这告诉软件给定组中的时钟与所有其他组是异步的。使用此方法，如果稍后添加 clk5，软件会将其视为与 clk1、clk2、clk3 和 clk4 异步。

如果您忘记时钟或稍后添加时钟，使用第二种方法可能很诱人。但是，无论您选择哪种方法，Efinix 都建议您在设计中***始终包含每个时钟的约束***，并在添加时钟时更新 SDC 文件。

#### Using the set_false_path Constraint

`set_false_path`约束可让您在设置时钟约束时更加具体。此约束允许您切断起点 （*from*） 和终点 （*to*） 之间的连接。frmo 和 to 可以是 registers (寄存器)、I/O 或 clocks (时钟)。

以下约束切断从 clk1 到 clk2 的连接：

```sdc
set_false_path -from clk1 -to clk2
```

但请记住，这只会切断一个方向的连接。要指定 clk1 和 clk2 之间没有关系，还需要使用以下约束：

```sdc
set_false_path -from clk2 -to clk1
```

---

**Example: Using set_false_path Constraints**

我们假设的四时钟设计所需的约束的完整示例是：

```sdc
set_false_path -from clk1 -to clk3 
set_false_path -from clk1 -to clk4 
set_false_path -from clk2 -to clk3 
set_false_path -from clk2 -to clk4 
set_false_path -from clk3 -to clk1 
set_false_path -from clk3 -to clk2 
set_false_path -from clk3 -to clk4 
set_false_path -from clk4 -to clk1 
set_false_path -from clk4 -to clk2 
set_false_path -from clk4 -to clk3
```

---

When you want to cut paths between clock domains, as in this simple example, Efinix recommends that you use `set_clock_groups` instead of `set_false_path`. The `set_false_path` constraint becomes more useful when you want to specify exceptions for registers or I/O, or if you want to cut only one direction of a clock domain pair.

---

**Example:  Cut Path to a Port or Pin**

To cut only the path from clk1 to a port named testout:

```sdc
set_false_path -from clk1 -to [get_ports testout]
```

To cut only the path from clk1 to a pin named testout:

```sdc
set_false_path -from clk1 -to [get_pins instance|testout]
```

---

#### Clock Synchronizers
# 设计流程

1. 设计规划
   * 了解项目需求
   * 划分子功能模块
   * **确定各子功能模块的输入输出信号**
   * **确定各子功能模块之间的结构关系和信号传递**
2. 波形绘制
   * 具体了解子功能模块的模块功能
   * 绘制子功能模块的模块框图
   * **搞清楚如何通过输入信号得到我们想要的输出信号**
   * **绘制出功能实现的时序波形图**
3. 代码编写
4. 代码编译
5. 逻辑仿真
6. 波形对比
7. 绑定管脚
8. 分析综合，布局布线
9. 上板验证

# 点亮LED灯

led模块

```verilog
module  led
(
    input wire key_in,
    output wire led_out
);

assign led_out = key_in;

endmodule
```

仿真模块

```verilog
`timescale 1ns/1ns
module tb_led();

// wire  define
wire led_out;

// reg  define
reg key_in;


// 初始化输入信号
initial key_in <= 1'b0;

// kye_in:产生输入随机数，模拟按键的输入情况
always #10 key_in <= ($random) % 2;

// led模块实例化
led led_inst
(
    .key_in (key_in),   //input key_in
    .led_out(led_out)   //output led_out
);

endmodule
```

# 简单组合逻辑——多路选择器

使用 verilog 完成一个2路选择器

**mux2_1.v**

```verilog
module mux2_1(
    input wire in_1,    // input_1
    input wire in_2,    // input_2
    input wire sel,     // select_signal

    output reg out      // output
);
// 第一种实现方式, if-else
always @(sel, in_1, in_2) begin
    if (sel == 1'b1) begin
        out = in_1;
    end
    else begin
        out = in_2;
    end
end
// 第二种实现方式, case
always @(*) begin
    case(sel)
        1'b1 :
            out = in_1;
        1'b0 :
            out = in_2;
        default :
            out = in_1;
    endcase
end
// 第三种实现方式, 三元运算符 ? :
assign out = (sel == 1'b1) ? in_1 : in_2;

endmodule
```



**tb_mux2_1.v**

```verilog
`timescale 1ns/1ns

module tb_mux2_1();

reg in_1;
reg in_2;
reg sel;

wire out;

initial begin
    in_1 <= 1'b0;
    in_2 <= 1'b0;
    sel <= 1'b0;
end

always #10 in_1 <= {$random} % 2;
always #10 in_2 <= {$random} % 2;
always #10 sel <= {$random} % 2;

initial begin
    $timeformat(-9,0,"ns",6);
    $monitor("@time %t:in_1 = %b, in_2 = %b, sel = %b, out = %b", $time, in_1, in_2, sel, out);
end

mux2_1 mux2_1_inst(
    .in_1(in_1),   
    .in_2(in_2),
    .sel(sel),

    .out(out)
);

endmodule
```

# 简单组合逻辑——译码器

实现一个简单的三八译码器

**decoder.v**

```verilog
module decoder(
    input wire in_1,
    input wire in_2,
    input wire in_3,

    output reg [7:0] out
);

always @(*) begin
    case ({in_1, in_2, in_3}) 
        3'b000:
            out = 8'b0000_0001;
        3'b001:
            out = 8'b0000_0010;
        3'b010:
            out = 8'b0000_0100;
        3'b011:
            out = 8'b0000_1000;
        3'b100:
            out = 8'b0001_0000;
        3'b101:
            out = 8'b0010_0000;
        3'b110:
            out = 8'b0100_0000;
        3'b111:
            out = 8'b1000_0000;
        default:
            out = 8'b0000_0000;
    endcase
end

endmodule
```

**tb_decoder.v**

```verilog
`timescale 1ns/1ns

module tb_decoder ();

reg in_1;
reg in_2;
reg in_3;

wire [7:0] out;

initial begin
    in_1 <= 1'b0;
    in_2 <= 1'b0;
    in_3 <= 1'b0;
end

always #10 in_1 <= {$random} % 2;
always #10 in_2 <= {$random} % 2;
always #10 in_3 <= {$random} % 2;

initial begin
    $timeformat(-9, 0, "ns", 6);
    $monitor("@time %t: in_1 = %b, in_2 = %b, in_3 = %b, out = %b", $time, in_1, in_2, in_3, out);
end

decoder docoder_inst(
    .in_1(in_1),
    .in_2(in_2),
    .in_3(in_3),

    .out(out)
);

endmodule
```

# 简单组合逻辑——半加器

两个一位输入，产生结果位和进制位。

**half_adder.v**

```verilog
module half_adder (
    input wire in_1,
    input wire in_2,

    output wire sum,
    output wire count
);

assign {count, sum} = in_1 + in_2;
    
endmodule
```

**tb_half_adder.v**

```verilog
`timescale 1ns/1ns
module tb_half_adder ();

reg in_1;
reg in_2;

wire sum;
wire count;

initial begin
    in_1 <= 1'b0;
    in_2 <= 1'b0;
end

always #10 in_1 <= {$random} % 2;
always #10 in_2 <= {$random} % 2;

initial begin
    $timeformat(-9, 0, "ns", 6);
    $monitor("@time %t: in_1 = %b, in_2 = %b, sum = %b, count = %b.", $time, in_1, in_2, sum, count);
end

half_adder half_adder_inst (
    .in_1   (in_1),
    .in_2   (in_2),
    .sum    (sum),
    .count  (count)
);

endmodule
```

# 层次化设计

数字电路电根据模块层次不同有两种基本的结构设计方法：

* 自底向上(Bottom-Up)的设计方法
* 自顶向下(Top-Down)的设计方法。

# 避免latch产生

latch：锁存器。这是一种在异步电路系统中，对输入信号电平敏感的单元，用来存储信息。

锁存器在数据未锁存时，输入端的信号随输入端变化，就像信号通过一个缓冲器，一旦锁存信号有效，则数据被锁存输入信号不起作用。因此锁存器又称为透明锁存器，指的是不锁存时输出对于输入的信号是透明的。

异步电路：

​		异步电路主要是组合逻辑电路，用于产生FIFO或RAM的读写控制信号脉冲，但它同时也用在时序电路中，此时他没有统一的时钟，状态变化的时刻是不稳定的，通常输入信号只在处于稳点状态时才发生变化。

同步电路：

​		同步电路：同步电路是由时序电路(寄存器和各种触发器)和组合逻辑电路构成的电路，其所有操作都是在严格的时钟控制下完成的。这些时序电路共享同一个CLK，而所有的状态变化都是在时钟的上升沿（或下降沿）完成的。

​		**latch在异步电路中是十分有用的，而在同步电路中则会产生一些不好的效果。**

## latch在同步电路中的危害

* 对毛刺敏感
* 不能异步复位
* 复杂的静态时序分析
* 占用更多的逻辑资源
* 额外的延时

## 几种产生latch的情况

* 组合逻辑中的if-else条件分支语句缺少else语句
* 组合逻辑中case条件分支语句未完全列举，且缺少default语句
* 组合逻辑中输出变量赋值给自己

# 时序逻辑的开始——寄存器

寄存器具有存储功能，一般是由D触发器构成，由时钟脉冲控制，每个D触发器(D Flip Flop, DFF)能够存储一位二进制码。

D触发器的工作原理：在一个脉冲信号（一般为晶振产生的时钟脉冲）上升沿或者下降沿的作用下，将信号从输入端D送到输出端Q，如果时钟脉冲的边沿信号未出现，即使输入信号改变，输入信号仍然保持原值，且寄存器拥有复位清零的功能，其复位又分为同步复位和异步复位。

**同步复位**

* 复位信号来临时，等待时钟信号的下一个跳变沿（上升沿或者下降沿可自行选择），进行复位。
* 复位信号结束后，等待时钟信号的下一个跳变沿（上升沿或者下降沿可自行选择），恢复运行。

**异步复位**

* 复位信号来临时，立即复位。
* 复位信号结束后，等待时钟信号的下一个跳变沿（上升沿或者下降沿可自行选择），恢复运行。

**组合逻辑**

* 输入信号的毛刺将直接体现在输出信号中。
* 输入信号与输出信号在时间上是同步变化的。
  * 如果时钟和数据的时钟沿是对齐的，则默认当前时钟沿采集的到的数据，是当前时钟沿的输入数据的值。（有问题，怎么能采集时钟沿呢，尝试用无时序的逻辑电路去理解）

**时序逻辑**

* 能有效避免输入信号毛刺带来的干扰
  * 时序逻辑在时钟信号相邻的两个上升沿（或下降沿）对输入信号进行采样。这种特性使得某个时钟周期内的输出信号的值不变。若在单个时钟周期内输入信号出现信号毛刺，则这种毛刺不会对输出信号产生影响。
* 输出信号的变化会比输入信号的变化慢一个时钟周期
  * 如果时钟和数据的时钟沿是对齐的，则默认当前时钟沿采集到的输入数据，是当前时钟沿前一时刻的输入数据的值。
* 时序逻辑中赋值一定要使用非阻塞赋值。

## 代码实现

### 同步复位

```verilog
module flip_flop (
    input wire sys_clk, //50MHz
    input wire sys_rst_n,
    input wire key_in,

    output reg led_out 
); 

// 同步复位
always @(posedge sys_clk) begin
    if(sys_rst_n == 1'b0)
        led_out <= 1'b0;
    else
        led_out <= key_in;
end

endmodule
```

**result**

![image-20240821170204669](FPGA.assets/image-20240821170204669.png)

### 异步复位

```verilog
module flip_flop (
    input wire sys_clk, //50MHz
    input wire sys_rst_n,
    input wire key_in,

    output reg led_out 
); 

// 异步复位
always @(posedge sys_clk or negedge sys_rst_n) begin
    if(sys_rst_n == 1'b0)
        led_out <= 1'b0;
    else
        led_out <= key_in;
end

endmodule
```

**result**

![image-20240821182739262](FPGA.assets/image-20240821182739262.png)

## 结论

通过对比同步复位和异步复位的综合出的D触发器的RTL视图，可发现如果使用同步复位会比使用异步复位多出一个选择器的结构，这样会消耗更多的逻辑资源。

我们的FPGA芯片厂家Altera(已被Intel收购)推荐我们使用异步复位。

# 阻塞赋值和非阻塞赋值

## 阻塞赋值

​		阻塞赋值的赋值号用 “=” 表示，对应的电路结构往往与出发边沿没有关系，只与输入电平的变化有关系。它的操作可以认为是只有一个步骤的操作，即计算赋值号右边的语句并更新赋值号左边的语句，此时不允许有来自任何其他Verilog语句的干扰，知道现行的赋值完成，才允许下一条的赋值语句的执行。

​		串行块(begin-end)中，各条阻塞赋值语句将以它们在顺序块中的排列次序依次执行。

```verilog
// a = 1, b = 2, c = 3,
begin 
	a = b + 1;
    b = a + 2;
    c = a - 1;
end
```

以上述代码为例，begin-end块中的代码依次执行。此时其他语句不执行。

上述计算a, b, c的结果分别为3, 5, 4

## 非阻塞赋值

​		非阻塞赋值的赋值号用"<="表示，对应的电路结构往往与触发沿有关系，只有在作为触发沿的时刻才能进行非阻塞赋值。

​		它的操作可以看作是两个步骤的过程：在赋值开始时刻，计算赋值号右边的语句。在赋值结束时刻，更新赋值号左边的语句。

​		在计算非阻塞赋值语句赋值号右边的语句和更新赋值号左边的语句期间，允许其他的Verilog语句同时进行操作。

​		在begin-end串行块之间，多个非阻塞赋值语句是并行执行的。

​		非阻塞赋值只能用于对寄存器类型变量进行赋值，因此只能用于"initial"和"always"块中，不允许由于连续赋值"assign"。

```verilog
// a = 1, b = 2, c = 3
begin
    a <= b + 1;
    b <= a + 2;
    c <= a - 1;
end
```

上述计算a, b, c的结果分别为3, 3, 0

## 实验验证

### 阻塞赋值

**代码**

```verilog
module blocking (
    input wire sys_clk,
    input wire sys_rst_n,
    input wire [1:0] in,

    output reg [1:0] out

);

reg in_reg;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0) begin
        in_reg = 2'b0;
        out = 2'b0;
    end
    else begin
        in_reg = in;
        out = in_reg;
    end
end

endmodule
```

**RTL综合结果**

![image-20240823171108412](FPGA.assets/image-20240823171108412.png)

**仿真波形**

![image-20240823175120866](FPGA.assets/image-20240823175120866.png)

中间变量`in_reg`在时钟变化时读到输入信号`in`的上一时刻的值，所以`in_reg`比`in`慢一个时钟周期。

而由于`out = in_reg`采用的是阻塞赋值，赋值过程中其他代码均被阻塞，所以`out`与`in_reg`同步变化。

猜想：由于阻塞赋值的过程中需要将其他代码进行阻塞，所以在高速时序逻辑电路中可能会出现问题。

### 非阻塞赋值

**代码**

```verilog
module blocking (
    input wire sys_clk,
    input wire sys_rst_n,
    input wire [1:0] in,

    output reg [1:0] out

);

reg [1:0] in_reg;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0) begin
        in_reg <= 2'b0;
        out <= 2'b0;
    end
    else begin
        in_reg <= in;
        out <= in_reg;
    end
end

endmodule
```

**RTL综合效果**

![image-20240823181055024](FPGA.assets/image-20240823181055024.png)

**仿真波形**

![image-20240823181030131](FPGA.assets/image-20240823181030131.png)

中间变量`in_reg`在时钟跳变时读到输入信号`in`上一时刻的值，所以`in_reg`比`in`慢一个时钟周期。

而由于`out <= in_reg`采用的是非阻塞赋值，所以`out`会在下一个时钟周期完成变化为`in_reg`这一时钟周期的值。

理解：通过时钟的严格控制来使赋值这种行为变得可预测。不会在高速时序逻辑电路中出现难以预料的问题。

## 官方推荐

在设计组合逻辑电路时使用阻塞赋值，在设计时序逻辑电路时使用非阻塞赋值。

## 编写RTL代码时推荐的规范

* 编写**时序逻辑**时采用**非阻塞赋值**的方式
* 使用**always语句块**来编写**组合逻辑**时，要使用**阻塞赋值**的方式
  * **敏感列表**使用**电平触发**的方式
* **在一个always语句块中不要既使用阻塞赋值，又使用非阻塞赋值**
* **一个always语句块只对一个变量进行赋值，这样方便后期维护和修改**
* **不推荐使用锁存器**
  * 如果**非要使用锁存器**，请一定使用**非阻塞赋值**的方式
  * 使用非阻塞赋值实现时序逻辑，进而实现锁存器是最为安全的。

## 总结

要理解**赋值**和**采样**的**不同**，条件判断式中的条件相当于采样，即在时钟边沿条件变量的值被采样并与条件做对比，之所以条件中含有非阻塞变量时会延后一个周期，本质是被采样的reg变量在其他模块使用了非阻塞赋值，而非阻塞赋值完成有两个步骤，在某一个仿真节拍（不是一个仿真周期），被采样的还没有赋值完成（处在RHS的计算阶段），而采样时同时进行，这样，采样到的就是上一个周期的reg变量的值，虽然马上在边沿完成赋值，但采样已经结束，故在这个仿真周期结束时，被采样的完成赋值，但条件分支（含有被采样reg的判断表达式）下的变量赋值在下一个周期得到目标值，故而表现为相对被采样的变量的赋值，延后一个周期完成赋值。

同理，条件分支下含有多条非阻塞赋值语句时，理解也是一样：在同一个仿真节拍（RHS的计算），下一条非阻塞赋值的变量non2的右端得得到的是上一周期的前一非阻塞赋值的reg的值（non1），而在第二仿真节拍（赋值），non2和non1得到的值就不是一样的，故non2会表现的延后一个周期。

-->总结：非阻塞赋值延后一个周期3种情况

1、条件分支中变量（不管是外部输入还是本模块的非阻塞reg型）的边沿对齐时钟边沿时，采样采的是上一周期的值（历史值），故分支内的非阻塞赋值会延后一个周期。

2、凡是出现在同步时序always块中，条件分支中出现非阻塞变量或者与时钟边沿对齐的情况，采用非阻塞赋值会使变量赋值延后一个周期。

3、多条非阻塞赋值语句；

**参考博客：**https://blog.csdn.net/huigeyu/article/details/93741425

# 计数器

计数是一种最简单的基本运算，计数器就是实现这种运算的逻辑电路，计数器在数字系统中主要是对脉冲的个数进行计数，以实现测量、计数和控制的功能，同时兼有分频功能。

计数器在数字系统中应用广泛，如电子计算机的控制器中队指令地址进行计数，以便顺序取出下一条指令，在运算器中做乘法、除法运算时记下加法、减法次数，又如在数字仪器中对脉冲的计数等等。

## 直接实现计数器

**代码**

```verilog
module counter #(
    parameter CNT_MAX = 25'd24_999_999
) (
    input wire sys_clk,
    input wire sys_rst_n,

    output reg led_out
);
reg [24:0] cnt;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        cnt <= 25'd0;
    else if (cnt == CNT_MAX)
        cnt <= 25'd0;
    else
        cnt <= cnt + 25'd1;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        led_out <= 1'b1;
    else if (cnt == CNT_MAX)
        led_out <= ~led_out;
    else
        led_out <= led_out;
end

endmodule
```

**波形图**

![image-20240826161814389](FPGA.assets/image-20240826161814389.png)

## 引出脉冲标志信号实现计数器

**使用脉冲信号的好处**

* 可以使代码中if-else的条件更加清晰简洁
* 当在多处需要使用脉冲标志信号的地方，比全部写出逻辑关系更节省逻辑资源

脉冲标志信号在指示某些状态时是非常有用的，当以后在实现相对复杂的逻辑功能时。

**代码**

```verilog
module counter #(
    parameter CNT_MAX = 25'd24_999_999
) (
    input wire sys_clk,
    input wire sys_rst_n,

    output reg led_out
);
reg [24:0] cnt;
reg cnt_flag;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        cnt <= 1'b0;
    else if (cnt == CNT_MAX)
        cnt <= 1'b0;
    else
        cnt <= cnt + 25'd1;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        cnt_flag <= 1'b0;
    else if (cnt == CNT_MAX - 25'd1)
        cnt_flag <= 1'b1;
    else
        cnt_flag <= 1'b0;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        led_out <= 1'b1;
    else if (cnt_flag == 1'b1)
        led_out <= ~led_out;
    else
        led_out <= led_out;
end    

endmodule
```

**波形图**

![image-20240826165304816](FPGA.assets/image-20240826165304816.png)

# 分频器

时钟对于FPGA来说是非常重要的，但是板载晶振提供的时钟信号的频率对于FPGA来说是固定的。

分频器是数字系统设计中最常见的基本电路之一。所谓“分频”，就是把输入信号的频率变成成倍数地低于输入频率的输出信号。

分频器分为偶数分频器和奇数分频器，和计数器非常类似，有时候甚至可以说就是一个东西。

## 偶分频——以六分频为例

### Plan A——借鉴计数器闪灯的思想

**代码**

```verilog
module divider_six(
    input wire sys_clk,
    input wire sys_rst_n,

    output reg clk_out
);
parameter CNT_MAX = 2'd2;

reg [1:0] cnt;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        cnt <= 2'b0;
    else if (cnt == CNT_MAX)
        cnt <= 2'b0;
    else
        cnt <= cnt + 2'd1;  
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        clk_out <= 1'b0;
    else if (cnt == CNT_MAX)
        clk_out <= ~clk_out;
    else
        clk_out <= clk_out;
end

endmodule
```

**上述代码存在的问题**

* 这种方法分频得到的时钟，表面上是对系统时钟进行了分频，产生了一个新的低频时钟，但实际上与真正的系统时钟还是有很大的区别的。
* 因为在FPGA中，凡是时钟信号都要连接到全局时钟网络，又称全局时钟树。它是FPGA厂商专为时钟路径而特殊设计的，它能够使时钟信号到达每个寄存器的时间都尽可能的相同，减少时序问题的产生。
* 而上述方式产生的低频信号并没有连接到全局时钟网络上。
* 但是外部晶振传入的时钟信号通过关键连接到了FPGA的专用时钟引脚上。自然就连接到了全局时钟网络上。
* 所以在系统时钟工作下的信号要比刚刚分频产生的时钟更容易在高速系统中保持稳定。

### 改进方法——Plan B——借鉴计数器的脉冲标志位的思想

可以考虑使用脉冲标志信号flag进行改进。

可以产生一个用于标记六分频的flag标志信号。这样每两个flag脉冲之间的频率就是对系统时钟的六分频。

**代码**

```verilog
module divider_six(
    input wire sys_clk,
    input wire sys_rst_n,

    output reg clk_flag
);
parameter CNT_MAX = 3'd5;

reg [2:0] cnt;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 0)
        cnt <= 3'b0; 
    else if (cnt == CNT_MAX)
        cnt <= 0;
    else cnt <= cnt + 1'b1;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 0)
        clk_flag <= 0;
    else if (cnt == CNT_MAX - 1'b1)
        clk_flag <= 1;
    else clk_flag <= 0;
end

endmodule
```

**波形图**

![image-20240829201021650](FPGA.assets/image-20240829201021650.png)

**改进之处**

两种分频方法在使用时有显著的区别。

Plan A 的使用：

```verilog
reg a;

always @(posedge clk_out or negedge sys_rst_n) begin
    if (sys_rst_n == 0)
        a <= 1'b0;
	else
        a <= a + 1'b1;
end
```

Plan B 的使用：

```verilog
always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        a <= 1'b0;
    else if (clk_flag == 1;b1)
        a <= a + 1'b1;
end
```

两种方法使用时的显著区别在于always语句中敏感列表的时钟信号的不同。

Plan A在使用时，敏感列表的时钟信号是`clk_out`。

Plan B在使用时，敏感列表的时钟信号是`sys_clk`。

`clk_out`是我们通过verilog语言分频实现的时钟，没有连接到全局时钟树，在高频电路中使用容易产生时序问题。

`sys_clk`是我们由晶振产生的系统时钟，连接在全局时钟树上，在高频电路中更容易保证时序的正确。

**所以在设计分频器时，推荐使用Plan B。**

## 奇分频——以五分频为例

### Plan A——采用或运算实现分频

**代码**

```verilog
/***********Plan A**********/
module divider_five(
    input wire sys_clk,
    input wire sys_rst_n,

    output wire clk_out
);
parameter CNT_MAX = 4;

reg [2:0] cnt;
reg clk_pos;
reg clk_neg;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        cnt <= 1'b0;
    else if (cnt == CNT_MAX)
        cnt <= 1'b0;
    else
        cnt <= cnt + 1'b1;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        clk_pos <= 1'b0;
    else
        case (cnt)
            3'd2: clk_pos <= 1'b1;
            3'd4: clk_pos <= 1'b0;
            default: clk_pos <= clk_pos;
        endcase
end

always @(negedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        clk_neg <= 1'b0;
    else
        case (cnt)
            3'd2: clk_neg <= 1'b1;
            3'd4: clk_neg <= 1'b0;
            default: clk_neg <= clk_neg;
        endcase
end

assign clk_out = (clk_neg | clk_pos);

endmodule
```

**波形图**

![image-20240831184012069](FPGA.assets/image-20240831184012069.png)

### Plan B——采用降频的手段

**代码**

```verilog
/**********Plan B************/
module divider_five(
    input wire sys_clk,
    input wire sys_rst_n,

    output reg clk_flag
);
parameter CNT_MAX = 4;

reg [2:0] cnt;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        cnt <= 3'b0;
    else if (cnt == CNT_MAX)
        cnt <= 3'b0;
    else
        cnt <= cnt + 3'd1;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        clk_flag <= 1'b0;
    else if (cnt == CNT_MAX - 3'b1)
        clk_flag <= 1'b1;
    else
        clk_flag <= 1'b0;
end

endmodule
```

**波形图**

![image-20240831184104836](FPGA.assets/image-20240831184104836.png)

# 按键消抖

常见的按键有自锁式按键和机械按键。

按键消抖主要针对的是机械弹性开关，当机械出点断开、闭合时，由于机械触点的弹性作用，一个按键开关在闭合时不会马上稳定地接通，在断开时也不会马上稳定的断开。

![image-20240831185937688](FPGA.assets/image-20240831185937688.png)

抖动时间的长短由按键的机械特性决定，一般为5ms~10ms。按键稳定闭合时间的长短则是由操作人员的按键动作决定的，一般为零点几秒至数秒。

按键抖动会引起一次按键被误读多次。为确保控制器对按键的一次闭合仅做一次处理，必须去除按键的抖动。在按键闭合稳定时读取按键的状态，并且必须判别到按键稳定释放再做处理。

## 硬件消抖

RS触发器或电容电路，详情可bing搜索。

## 软件消抖

**波形图**

![image-20240831203852021](FPGA.assets/image-20240831203852021.png)

**代码**

```verilog
module key_filter
#(
    parameter CNT_MAX = 20'd1_000_000
)
(
    input wire sys_clk,
    input wire sys_rst_n,
    input wire key_in,

    output reg key_flag
);
reg [19:0] cnt_20ms;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        cnt_20ms <= 20'b0;
    else if (key_in == 1'b1)
        cnt_20ms <= 20'd0;
    else if (cnt_20ms == CNT_MAX)
        cnt_20ms <= CNT_MAX;
    else
        cnt_20ms <= cnt_20ms + 20'd1;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        key_flag <= 1'b0;
    else if (cnt_20ms == CNT_MAX - 20'd1)
        key_flag <= 1'b1;
    else
        key_flag <= 1'b0;
end

endmodule
```

**仿真代码**

```verilog
module tb_key_filter();
reg sys_clk;
reg sys_rst_n;
reg key_in;
reg [7:0] tb_cnt;

wire key_flag;

initial begin
    sys_clk <= 1'b1;
    sys_rst_n <= 1'b0;
    #20 
    sys_rst_n <= 1'b1;
end

always #10 sys_clk = ~sys_clk;

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 1'b0)
        tb_cnt <= 8'b0;
    else if (tb_cnt == 8'd249)
        tb_cnt <= 8'd0;
    else
        tb_cnt <= tb_cnt + 1'd1;
end

always @(posedge sys_clk or negedge sys_rst_n) begin
    if (sys_rst_n == 0)
        key_in <= 1'b1;
    else if ((tb_cnt >= 8'd19 && tb_cnt <= 8'd49) || (tb_cnt >= 8'd149 && tb_cnt <= 8'd199))
        key_in <= {$random} % 2;
    else if (tb_cnt <= 8'd19 || tb_cnt >= 8'd199)
        key_in <= 1'b1;
    else
        key_in <= 1'b0;
end

key_filter #(
    .CNT_MAX   (20'd24)
)
key_filter_inst 
(
    .sys_clk   (sys_clk   ),
    .sys_rst_n (sys_rst_n ),
    .key_in    (key_in    ),
    .key_flag  (key_flag  )
);

endmodule
```


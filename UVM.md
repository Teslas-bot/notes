# UVM的基本概念

UVM -- Universal Verification Methodology -- 通用验证方法学

基于System Verilog

## UVM的特点

- 一个标准的验证平台的模板
- 一套完备的源码库
- 支持受约束随机激励的产生
- 支持覆盖率驱动的验证模式
- 代码可重用，平台可移植

## UVM提供的资源

UVM的基础是一个源码库，这个源码库为用户提供了各种资源

1. 编程指导
   * 理念
     * 可在同一个平台上进行多种验证
     * 由覆盖率驱动的验证
   * 功能
     * UVM factory
     * UVM TLM
     * 信息服务
     * Configuration机制
     * Phase
     * RAL
     * ……
2. 验证组件
   * uvm_component
   * uvm_driver
   * uvm_monitor
   * uvm_sequencer
   * uvm_agent
   * uvm_env
   * uvm_test
   * ……
3. 验证激励
   * uvm_sequence
   * uvm_sequence_item
   * ……
4. 通信机制
   * uvm\_*\_port
   * uvm\_*\_export
   * uvm\_*\_import

5. 宏
   * `uvm_info()
   * `uvm_component_utils()
   * `uvm_field_*()
   * ……

**UVM验证平台是一种可重用性极强的平台，每个基于UVM的验证平台结构大同小异**

## 典型的UVM平台结构

![image-20250713084157470](UVM.assets/image-20250713084157470.png)

若搭建多个模块存在的UVM平台，则需要在各个模块中间加入passive agent。

![image-20250713084256966](UVM.assets/image-20250713084256966.png)

# 搭建一个简单的UVM平台

## UVM平台的主要组件

![image-20250713084157470](UVM.assets/image-20250713084157470.png)

以测试单个模块搭建的UVM为例，介绍UVM平台的主要组件。

* driver - 将获取到的事务转化为pin级信号驱动DUT
* sequencer - 启动sequence产生事务，并将事务发送给driver
* monitor - 检测接口上的有效信号，并转化为事务，再发送到reference model进行分析。
* agent - 将sequencer, driver和monitor封装起来。agent中的driver和sequencer需要连接起来。
* reference model - 模拟DUT的功能行为，根据激励来产生结果，该结果被称为参考值或是期望值。master agent 中的monitor会将DUT的输入收集下来发送给reference model，作为reference model的输入。该结果会送入scoreboard中做比对。
* monitor - slave agent中的monitor往往是捕获DUT的输出信号并转化为事务的功能组件。一般情况下，因为slave agent不需要驱动DUT，所以说他只包含monitor而去除了driver以及sequencer。我们称这种只有monitor的agent为agent的passive模式
* scoreboard - 比较预期的结果于DUT的输出结果是否一致。它将会从两个地方获取数据，一个是参考模型发来的期望值，另一个是从slave agent发来的DUT的输出值。在scoreboard中对这两个值进行比较，由此来判断DUT的功能是否正确。同时可以将功能覆盖率嵌入到scoreboard中，由此实现覆盖率的收集。
* env- 可包含多个agent, reference model, scoreboard以及其他连接组件和配置组件。**需要注意的是**：一旦env完成，在后续的测试案例中，就不能对它进行更改。如果出现必须更改的情况，那么之前已经通过的测试案例需要重新执行。
* testcase - 测试案例。实例化env，配置env，启动测试平台。在一个测试项目当中，测试案例可以有很多，但是env只有一个，并且一旦确定就不能随意更改，对于整个平台的配置都是在测试案例中完成的。**因此在构建env的时候，需要事先定义好配置接口，使env具有可配置性。**

UVM不仅为验证工程师提供了测试平台的结构，而且在UVM的资源库当中，对于平台中的每一个组件都有一个对应的基类。验证工程师在搭建验证平台的时候，每一个组件需要从相应的基类进行扩展。下面来看一下UVM提供了哪些基类，以及这些基类和平台中的各个组件之间的关系。

* 构成平台的结构组件
  * uvm_component - 所有组件的基类
    * uvm_test - 对应着testcase测试案例。验证工程师的测试案例都是从这个基类扩展而来的。
    * uvm_env - 对应着env。平台的env需要从这个基类扩展。
    * uvm_scoreboard - 对应着scoreboard。平台的scoreboard需要从这个基类扩展
    * uvm_agent - 对应着agent。平台的agent需要从这个基类扩展
    * uvm_suquencer
    * uvm_monitor
    * uvm_driver

需要主要的是，UVM并未提供类似uvm_reference_model这样的基类。所以用户在编写例化自己的reference_model模块时，需要继承uvm_component这个基类加以扩展。

* 组件间的通信端口
  * uvm\_*\_port
  * uvm\_*\_import
  * uvm\_*\_export
  * uvm\_\*\_fifo\_\*
  * uvm\_\*\_fifo\_socket

如果将验证平台的组件比作工厂中流水线的设备，那么事务就是穿梭于这些设备之间的产品了。事务是组件的操作对象。UVM也对事务的建模提供了扩展。

* uvm_sequence_item - 对事务级的建模，需要从此类进行扩展
* uvm_sequence - 产生事务对象的事务发生器sequence，需要从uvm_sequence扩展

## 简化UVM平台

![image-20250717090824833](UVM.assets/image-20250717090824833.png)

这个简化后的UVM平台的功能是

* 产生事务
* 将产生的事务发送到driver上面

## 创建transaction - 事务级建模

在UVM验证平台中，穿梭于各个组件之间的基本信息单元是一个被称为transaction的数据对象。也就是我们前面所说的事务对象。那么在本课程中，说**事务就是transaction**。

**定义transaction**

* 需要从uvm_sequence_item扩展
* 为了使transaction能够随机化，需要为每个成员指定为rand

```systemverilog
class my_transaction extends uvm_sequence_item;
    // 需要为激励成员指定rand属性使他们是随机的
    // 源地址
    rand bit [3:0] source_addr;
    // 目标地址
    rand bit [3:0] dest_addr;
    // 传输的数据
    rand reg [7:0] payload[$];
    
    // 使用UVM提供的宏，将自定义的事务类向UVM注册
    `uvm_object_utils_begin(my_transaction)
    	`uvm_field_int(source_addr, UVM_ALL_ON)
    	`uvm_field_int(dest_addr, UVM_ALL_ON)
    	`uvm_field_queue_int(payload, UVM_ALL_ON)
    `uvm_object_utils_end
    
    // 约束项，控制随即成员的随机范围
    constraint Limit{
        // 限制source_data的值只能在0~15之间随机
        source_addr inside {[0:15]};
        // 限制dest_data的值只能在0~15之间随机
        dest_addr inside {[0:15]};
        // 限制payload这个队列当中，最大的内容为4个，最小为2个
        payload.size() inside {[2:4]};
    }
    
    // 构造函数
    // 参数name是实例化时为该对象指定的名字
    fucntion new (string name = "my_transaction");
    	// 使用父类evm_sequence_item的构造函数进行实例化
    	super.new(name);
    endfunction
    
endclass
```

## 创建sequence - 事务发生器

当事务模型创建好之后，需要创建的对应的事务发生器，在UVM当中，这个事务发生器就是sequence。在平台的运行过程当中，只有启动了某个sequence，才会产生相应的事务对象。

创建对应的sequence需要注意以下几点：

* sequence需要从uvm_sequence扩展
* sequence控制并产生一系列sequence，并且可以控制事务何时产生，何时结束
* 一种sequencec一般只用来产生一种类型的transaction
* sequence中最重要的部分就是body()任务。对事务的控制和事务的产生都是在这个body()任务中完成的。因此写好body()任务时关键。

当一个sequence被启动后，他会按照body()函数中的功能，依次产生多个相同类型的事务对象。

![image-20250717095906514](UVM.assets/image-20250717095906514.png)

```systemverilog
// uvm_sequence是一个带有参数的基类，该参数是指定sequence所产生的事务类型
class my_sequence extends uvm_sequence #(my_transaction);
    
    // 使用uvm提供的宏将此sequence注册到UVM中
    `uvm_object_utils(my_sequence)
    
    // 构造函数
    function new(string name = "my_sequence");
        super.new(name);
    endfunction
    
    // body()任务是sequence中最重要的一个方法，它的作用是控制和产生transaction序列。需要验证工程师自己编写
    // 这里给出的例子十分简单，开始仿真，产生10个事务对象，停止仿真
    virtual task body();
        // 控制验证平台何时开始
        if (starting_phase != null)
            starting_hpase.raise_objection(this);
        
        // repeat这个宏语句10次，一共会产生10个transaction
        repeat(10)begin
            // UVM内建的宏，用来产生transaction。每调用一次产生一个transaction
            // 宏当中的参数req是指向产生事务对象的指针
            // 我们可通过req来访问产生的事务对象
            `uvm_do(req)
        end
        
        #100;
        // 控制验证平台何时结束
        if (starting_phase != null)
            starting_phase.drop_objection(this);
    endtask
        
```

## 创建sequencer

从UVM的平台结构的角度看，sequence_item和sequence并不属于结构的一部分。它们是流动在 这些组件中的数据流。

uvm_sequencer的作用：

* 启动sequence - 一个sequnece不能自己启动其中的body()方法来产生事务对象。必须由一个与之相关联的sequencer来启动。
* 将sequence产生的item(transaction)发送到UVM的组件中（具体来说，就是发送到driver中）。

sequencer的功能大多数已经在UVM源码中实现，所以创建sequencer的工作是比较简单的。

在多数情况下，我们不需要从uvm_sequencer基类中扩展新功能，此时则不需要自定义一个新的子类继承uvm_sequencer。此时可以用typedef关键字来对uvm_sequencer进行重命名来以简化拼写。例如：

```systemverilog
typedef uvm_sequencer #(my_transaction) my_sequencer;
```

一个参数化的类，一般需要指定sequencer传递的transaction类型，便是一种sequencecr对应一种类型的transaction。

## 创建driver

## 创建monitor

## 创建monitor

## 创建agent

## 创建environment

## 创建testcase

## 运行仿真
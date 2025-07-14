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
* monitor - slave agent中的monitor往往是捕获DUT的输出信号并转化为事务的功能组件。

## 创建用户所需的transaction

## 创建sequence

## 创建sequencer

## 创建driver

## 创建monitor

## 创建monitor

## 创建agent

## 创建environment

## 创建testcase

## 运行仿真
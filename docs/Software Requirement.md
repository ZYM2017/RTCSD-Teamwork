**软件需求规范文档**
**Software Requirements Specifications Document (SRS)**

> 本文档参照IEEE Guide to Software Requirements Specifications (Std 830-1993). 本文档只用于定义软件的需求分析、功能和接口定义，不涉及软件的具体实现方法。

- 项目名称：**咖啡机的嵌入式控制软件**

- 开发团队：Eudoray

- 版本号：(1.0)	

- 日期： (10/22/2017)


# 1. 引言

## 1.1 编写目的

本文档用于指导咖啡机的嵌入式控制软件开发过程，与软件用户定义和明确软件的功能需求。本文档的目标读者为软件用户和软件开发项目组成员。

## 1.2 背景

### 1.2.1 立项目标
为某创业公司正在设计的一台自动咖啡机开发出嵌入式控制软件，实现相关的功能要求
### 1.2.2 类似产品分析

## 1.3 参考资料

- Github项目管理相关教程
- Matlab/Simulink官方相关教程
- <<构建之法>>

# 2. 任务概述

## 2.1 目标

1）用户在咖啡机面板上选择自己想要喝的咖啡（美式、拿铁、卡布奇诺...）并按下开始按钮后，咖啡机开始按照设定的配方制作咖啡。
2）制作流程为：Feeder机构取一空杯放到传送带上，传送带把空杯送到龙头下，牛奶、糖浆、浓缩咖啡液和热水按照配方比例混合后装入空杯，传送带把满杯的咖啡送到用户取杯处，用户取走咖啡后，自动咖啡机可以继续响应面板上的按钮制作下一杯咖啡。要功能，与控制系统其他部件的关系。

## 2.2 用户的特点

不论男女老少，喜爱咖啡的大众
## 2.3 假定和约束

- 实验条件： STM32F4Discovery开发板，电脑
- 开发期限：2017年11月完成软件开发。
- 开发流程：按照软件流程规范，进行需求分析文档撰写和评审、系统架构方案撰写和评审、单元模块代码开发和单元测试、软件集成测试、现场调试和bug修复等工作。

# 3. 需求规定

## 3.1 功能需求规定

### 3.1.1 功能1

#### 功能描述：取出一个空杯

#### 输入：控制器的开始信号
#### 参数：start_up;

#### 处理过程：接受输入信号，控制上下移动电机下移，取下杯子，控制旋转电机旋转180°，放下杯子，控制上下电机上移，完成一个步骤的循环。
#### 输出：motor1、motor2

### 3.1.2 功能2

#### 功能描述：传送带输送杯子

#### 输入：三个位置传感器的信号、一个冲泡模块的冲泡完成信号
#### 参数：sensor1, sensor2, sensor3, chongpao_finished

#### 处理过程：第一个位置传感器接收到信号，控制传送带电机运行，传送带开始输送杯子，直到杯子运动至混合口下方，第二个位置传感器接收到信号，传送带电机停止。此时向冲泡模块发送杯子到位信号，控制冲泡模块开始工作。当接受到冲泡模块冲泡完毕的信号后，传送带电机开始运行。当传送带上的杯子运行到出口位置，第三个位置传感器接收到信号，传送带电机停止运行。
#### 输出：motor3

### 3.1.3 功能3

#### 功能描述：冲泡咖啡

#### 输入：咖啡种类信号、一个位置传感器信号
#### 参数：type, sensor4

#### 处理过程：接收到杯子到位信号后，读取咖啡种类信号，确定各个成分的配比，转化为对应的电磁阀和水泵开启持续时间。按照对应时间开启和关闭电磁阀和水泵。待冲泡完毕后，延时一段时间后，给模块二发送冲泡完毕的信号。
#### 输出：Doser1, Doser2, Doser3, Pump

### 3.1.4 功能4

#### 功能描述：水温控制

#### 输入：温度传感器信号，设定温度值
#### 参数：temper_cur, temper_des

#### 处理过程：接收到杯子到位信号后，读取咖啡种类信号，确定各个成分的配比，转化为对应的电磁阀和水泵开启持续时间。按照对应时间开启和关闭电磁阀和水泵。待冲泡完毕后，延时一段时间后，给模块二发送冲泡完毕的信号。
#### 输出：Doser1, Doser2, Doser3, Pump

### 3.1.5 功能5

#### 功能描述：用户交互

#### 输入：咖啡种类开关信号、取出口传感器信号
#### 参数：switch, sensor5

#### 处理过程：通过取出口传感器确认取出口没有咖啡的情况下，用户按下咖啡种类按钮后，向模块一输出开始工作信号，向模块三输出咖啡种类信号。
#### 输出：Start_up, type

## 3.2 性能需求的规定

### 3.2.1 精度要求
主要是冲泡咖啡时各成分的用量，热水温度

### 3.2.2 实时性要求
要求不高

### 3.2.3 开放性和扩展性
支持多种咖啡（不同比例和原料）的冲泡，用户操作界面可更新

## 3.3 输入输出要求

### 硬件接口：
I/O口，通信接口

### 软件接口：
待定

# 4 运行环境规定
## 4.1 硬件设备及接口
STM32F4
## 4.2 软件平台及配置
Matlab/Simulink
## 4.3 通信协议
待定

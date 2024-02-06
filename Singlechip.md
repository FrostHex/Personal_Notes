# 单片机

## 时钟
#### APB1 peripheral clocks 和 Timer clocks：
- APB1 Peripheral Clocks（APB1外设时钟）：
   - APB1 Peripheral Clocks 是系统总线上的一个时钟域，它提供了对一系列外设（如串口、SPI、I2C等）的时钟信号。
   - 这个时钟域的频率通常由系统时钟源（一般是HSI、HSE、PLL等）分频得到，因此它的频率不同于主时钟（SYSCLK）。
   - 这个时钟域可以通过设置RCC（Reset and Clock Control）寄存器来调整其频率分频比例，以满足外设的时钟要求。

- Timer Clocks（定时器时钟）：
   - Timer Clocks 是专门为定时器模块（如TIM1、TIM2、TIM3等）提供的时钟信号。
   - 定时器时钟通常直接来自于APB1 Peripheral Clocks，但在一些情况下，也可以来自APB2 Peripheral Clocks。
   - 定时器时钟的频率可以通过分频器来配置，以满足具体的定时器应用需求。这使得您可以根据应用的需要调整定时器的工作频率。

APB1 Peripheral Clocks 是供一系列外设使用的时钟信号，而Timer Clocks 是用于定时器模块的时钟信号。定时器时钟通常从APB1 Peripheral Clocks派生，但可以通过分频来调整，以适应不同的定时器应用需求。这种分层的时钟结构可以为不同类型的外设提供不同的时钟频率，以满足它们的工作要求。



## Cmakelists
#### 构建类型
构建类型用来指定编译器的优化级别和调试信息的生成。不同的构建类型会影响程序的性能和可调试性。

相比debug模式，release模式的不同点在于：
- 开启更高级别的优化，使得程序运行更快，但也会增加编译时间。
- 去掉调试信息，使得程序占用更少的空间，但也会导致无法使用调试器进行断点和变量查看。
- 关闭断言，使得程序更稳定，但也会忽略一些潜在的错误。

一般来说，release模式适合发布给用户使用，而debug模式适合开发和测试阶段。

`set(CMAKE_BUILD_TYPE "Release")`
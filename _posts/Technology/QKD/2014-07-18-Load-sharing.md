---
layout: post
title:  "共享负载--高频大信号放大解决方案"
category: 技术
tags: CV-QKD OP-Amp
---
#高频大信号放大解决方案：共享负载
###一、什么是“大信号”
对于±5V供电的运放，2Vpp即为大信号

对于±15V供电的运放，5Vpp即为大信号

然而，大信号的实际表现需要根据实际情况确定：

比如对于ADC驱动放大器，如低电压，±5V供电，全差分电压反馈放大器，则指定大信号带宽为2Vpp，因为2Vpp是通常情况下的ADC信号幅度。

另一方面，一个高电压正负28V电流反馈放大器(THS6204)，则大信号应用为4Vpp到20Vpp输出。

实际上，输出电压摆幅对于信号带宽的限制作用大于50%。

在大信号应用中，**电压摆率**对信号带宽的影响更大！
###二、摆率、输出电压摆幅、输出电流
三者是大信号应用中的关键参数，尤其是需要输出信号的失真很小时。以下简要总结它们之间的关系：

1. 摆率和大信号带宽直接相关。同时也与放大器的失真相关。从经验上讲，要支持一个80dBc(用来度量信号与载波功率之间的比值)的信号，则需要运放的摆率需要是能够支持该频率信号的摆率的20倍！

2. 放大器输出电流带载(output current sourcing and sinking ability into the load)能力决定了输出电压的摆幅。负载电流越大则失真越严重。另外，高速大摆幅信号加载到容性负载上时需要快速地对电容充放电，对于这种容性负载，运放有限的带载能力所带来的不足可以等同于视为摆率的降低。

3. 摆幅接近运放的双轨时输出同样会失真。

###三、负载共享运放
一个实际应用：

![interpreter pattern](/public/upload/Load-sharing/f1.png)

其中，两个运放的输出端均连接了100Ω的电阻，这样从GND看这两个电阻并联，并与50Ω的负载相匹配。
    
输出端的阻抗匹配嫩巩固使负载端的反射最小，也造成了6dB的负载端信号衰减。

输入端的匹配同样通过两个100Ω的电阻并联实现。

在实际应用中，即使不需要终端匹配和反向终端(back or double termination)，在两个运放的输出端放置一个电阻仍然是有必要的，它们能够使两个运放的输出电流达到平衡，防止反灌现象。

###四、 输出直流偏置
共享负载的应用需要避免运放之间的电流传输，否则会给整个电路造成致命伤害！

同时，即使由于共享负载使得每个运放的输出电流减小了，但是输出电压摆幅的要求却始终没变！

造成输出不均衡的一个原因便是输出信号的直流偏置。计算公式可参照《tidu153.pdf—P4》。

虽然双运放封装的放大器相对于单运放封装的运放具有更好的匹配特性，但是由于共享电源的不相互独立的限制，导致双运放封装并不适合在应用在共享负载中。这是由于它们共用一根电源管脚，可能会导致相互之间的正反馈（positive feedback）并进而导致振荡。选择单运放封装的另一个原因是散热问题，单运放封装可以的每个运放可以承载更大的功率。

**ps:**a double-terminated, 50 Ω cable：

![interpreter pattern](/public/upload/Load-sharing/f2.png)





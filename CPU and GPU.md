# 1 CPU 和 GPU 的基础知识
## 1 处理器指标

处理器结构，有2个指标是经常要考虑的：延迟和吞吐量。
所谓延迟，是指从发出指令到最终返回结果中间经历的时间间隔。
而所谓吞吐量，就是单位之间内处理的指令的条数。

## 2 CPU结构的几个特点：

1. CPU 中包含了多级高速的缓存结构。 因为我们知道处理运算的速度远高于访问存储的速度，那么奔着空间换时间的思想，设计了多级高速的缓存结构，将经常访问的内容放到低级缓存中，将不经常访问的内容放到高级缓存中，从而提升了指令访问存储的速度。
2. CPU 中包含了很多控制单元。 具体有2种，一个是分支预测机制，另一个是流水线前传机制。
3. CPU 的运算单元 (Core) 强大，整型浮点型复杂运算速度快。
* 因此cpu在设计时的导向就是减少指令的时延，我们称之为延迟导向设计
[
](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gYUsOT36vfrk55w9cPEoHKZyzE4VWJAfS0t1qwPs183jlfdncANrIDecUTz1W5walRgsEa58j11GelkesYuWGQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)![image](https://user-images.githubusercontent.com/99408013/183676233-22d14418-e441-4cb3-9e7e-51d6ca4854f3.png)

## 3 GPU结构的几个特点

1. GPU中虽有缓存结构但数量少
2. GPU中控制单元非常简单，控制单元中也没有分支预测机制和数据转发机制，对于复杂指令的运算就会非常缓慢
3. GPU的运算单元非常多，采用长延时流水线以实现高吞吐量，每一行的运算单元的控制器只有一个，意味着每一行运算单元执行的指令都是相同的，而不同的则是他们的数据内容，那么这种整齐划一的运算方式使得GPU对那种控制简单但运算高效的指令的效率大大增加
* 因此GPU的设计导向就是增加简单指令的吞吐，因此我们称GPU为吞吐导向设计
[
](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gYUsOT36vfrk55w9cPEoHKZyzE4VWJAfvaicPic6layBp4YQmkpoiaia3fDx1CPhSE7f1sCPEfkI7hn3tkbyKicibibww/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)[![image](https://user-images.githubusercontent.com/99408013/183676168-e3b80548-f6f2-48f3-9f21-3ba3f8decfe9.png)

[
](https://mmbiz.qpic.cn/sz_mmbiz_jpg/gYUsOT36vfrk55w9cPEoHKZyzE4VWJAfNribvOsbI0PRTia7fymJib6WknWgwjYgBZIuGMn4Fco5ZpPasoMml7ibjA/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1&wx_co=1)![image](https://user-images.githubusercontent.com/99408013/183676540-2f863f86-1ad6-40a0-8fea-f5cb7b82d258.png)

# 4 CPU与GPU适合的问题

cpu：连续计算问题，延迟优先，单条复杂指令的处理

gpu：

a.计算密集型：数值计算的比例远大于内存操作，因此对内存的访问延时可以被计算掩盖.  

b.数据并行型：大任务可以分解为执行相同简单指令的小任务，因此对复杂流程控制的需求较低







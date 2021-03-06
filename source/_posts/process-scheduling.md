---
title: 进程调度
date: 2019-04-10 14:38:56
tags: os
---

### 调度策略
+ *FCFS（先来先服务）*：当每个进程就绪后，加入就绪队列。当前正在运行的进程停止执行时，选择在就绪队列中存在时间最长的进程执行。执行长进程比短进程好，通常与优先级策略相结合。  
+ *轮转*：以一个周期性间隔产生时钟中断，当中断发生时，当前正在运行的进程被置于就绪队列中，然后基于FCFS策略选择下一个就绪作业运行。  
> 虚拟轮转法：解除了IO阻塞的进程都被转移到一个FCFS辅助队列中，当进行一个调度决策时，辅助队列中的进程优先于就绪队列中的进程。  
+ *最短进程优先（非抢占）*：下一次选择预计处理时间最短的进程，需要预先直到每个进程所需要的处理时间。  
+ *最短剩余时间（抢占）*：选择预期剩余时间最短的进程。存在长进程长期饥饿的危险。
+ *最高响应比优先*：调度规则在当前进程完成或被阻塞时，选择R=（w+s）/s最大的就绪进程。（w为等待处理器的时间，s为预计的服务时间）。当偏向短作业时，长进程由于w的不断增加，从而增大比值赢得短进程。  
+ *反馈*：调度基于抢占原则并且使用动态优先级机制。当一个进程第一次进入系统中时，被放置在RQ0，当它第一次被抢占后并返回就绪状态时，放到RQ1。在随后的时间里，每当它被抢占时，它被降级到下一个低优先级队列中。
> 一个短进程会很快执行完，不会在就绪队列中降很多级。一个长进程会逐级相加。因此新到的进程和短进程优先于老进程和长进程。  


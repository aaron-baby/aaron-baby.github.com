---
layout: post
title: Goroutines和Threads线程的区别
tags: goroutine thread
---
## {{page.title}} ##
> OS thread has a ﬁxed-size block of memory (often as large as 2MB) for its stack

> 线程（英語：thread）是操作系统能夠進行運算调度的最小單位。大部分情况下，它被包含在进程之中，是进程中的實際運作單位

> In contrast, a goroutine starts life with a small stack, typically 2KB. a goroutine’s stack is not ﬁxed; it grows and shrinks as needed.

> stack, the work area where it saves the local variables of function calls that are in progress or temporarily suspended while another function is called.

### 区别一，goroutine的栈是可以弹性伸缩的，而线程的栈是固定大小

> OS threads are scheduled by the OS kernel
> Every few milliseconds, a hardware timer interrupts the processor, which causes a kernel function called the scheduler to be invoked.

> Because OS threads are scheduled by the kernel, passing control from one thread to another requires a full context switch, that is, saving the state of one user thread to memory, restoring the state of another, and updating the scheduler’s data structures.

> The Go runtime contains its own scheduler that uses a technique known as m:n scheduling, because it multiplexes (or schedules) m goroutines on n OS threads.

### 区别二，goroutine有自己的调度器使用m:n模型，在n个系统线程上多路复用m个例程(routine)，可以使用`GOMAXPROCS`参数来指定使用多少个系统线程同步运行go代码。线程是系统内核调度的，调度器被硬件时钟唤醒，切换上下文

> In most operating systems and programming languages that support multithreading, the current thread has a distinct identity that can be easily obtained as an ordinary value, typically an integer or pointer. This makes it easy to build an abstraction called thread-local storage, which is essentially a global map keyed by thread identity, so that each thread can store and retrieve values independent of other threads.

> Goroutines have no notion of identity that is accessible to the programmer.

### 区别三，goroutine没有办法被识别和访问。线程可以比较容易的使用[线程局部存储](https://zh.wikipedia.org/wiki/%E7%BA%BF%E7%A8%8B%E5%B1%80%E9%83%A8%E5%AD%98%E5%82%A8)，因为线程是可标识的，通常整型或指针表示
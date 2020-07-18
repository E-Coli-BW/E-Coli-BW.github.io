---
layout: post
title:  "Some Notes on Several Concepts I always feel vague about"
date:   2020-07-17 00:15:07 -0400
tags: concurrency,parallelization notes, learning
categories: [concurrency,parallelization notes, learning]
---

# Programming-wise concepts

1. Thread vs Process vs Coroutines 

* Coroutine: sequential processing. one task gets executed at any given moment

* Threads: concurrent processes, multiple threads may be running at any given moment. (Note: single core can also do multithreading via slicing)

* Process: Both processes and threads are independent sequences of execution. However, thread **shares** memory space, process runs in **seperate** memory spaces

**Key difference between Coroutine and Thread**: 

Coroutine switches context **cooperatively** meaning the **programmer/programming language/runtime** controls when a switch happens.

Thread swtiches context preemptively, meaning **kernel** is scheduling(controls) the context-switching

**Some examples**:

Cotoutine: C# task, Python generator i.e: programmers can control when an object stops running and handle the control to sth else. OS kernels **does not** involve in this context-swithing/scheduling

Thread: Java multi-thread programming API, you can control thread on high level but the actual context-switching is done by the kernel

**Why coroutine if we already have thread?**

see [here](https://stackoverflow.com/questions/1934715/difference-between-a-coroutine-and-a-thread), short answer: co-routines have less overhead than thread due to the fact that co-routine don't need kernel scheduler to work.

ref: 
1) [StackOverflow: Difference between a coroutine and a thread](https://stackoverflow.com/questions/1934715/difference-between-a-coroutine-and-a-thread)
2) [StackOverflow: What is the difference between a process and a thread?](https://stackoverflow.com/questions/200469/what-is-the-difference-between-a-process-and-a-thread)



2. Concurrency vs Parallelization

* Concurrency means two or more tasks start, run, and complete in overlapping time periods. It may **NOT necessarily** be running at the same time 

e.g: multi-tasking on a single-core

* Parallelization means tasks are really running at the same time

e.g.: multi-tasking on a multi-core(if well programmed so parallelization can actually take place on difference cores)

ref: [stackoverflow](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism)

3. Some examples of Multi-thread, Multi-process, Coroutines

* multi-thread: Spark
* multi-process: Hadoop
* coroutines: C# tasks

# Some follow up on previous section

1. Coroutine vs Asynchrounous pattern?

Particularly in JavaScript we have callback/Promise/Async Await which all boils down to Asynchrounous programming.

Asynchrounous basically means during the flow of execution, you can pause some of the code block and wait for it to continue running from where it has been left off when a specific event happens(that triggers the callback function to run)

Coroutine is more of a threading thing and **Threading is about workers; asynchrony is about tasks. **


2. Aynchronous vs Multithreading vs Multiprocessing?
My Own Analogy(might be wrong):

Asynchronous: You hire one librarian("worker") handling the borrowing and returning of all the books ("tasks"). The working pattern of this librarian is asynchronous. It can pause at certain tasks and wait for response to return and continue working on it.

Multithread: You hire many librarians working for you. Each librarian can do the work and they all know about the resources in your library when a customer come.

Multiprocessing: You hire many librarians. Each librarian is responsible for **his own** section. When a customer come, he can ask certain librarians(not all, as not all of them knows the same thing (not sharing memory) ) for certain books. It still works in paralell but each librarian no longer sits on the same ground(know the same memory infomation)


# OS/kernel-wise concepts

These concepts are more of a OS/kernel thing rather than programming 

1. Kernel Space, User Space, Heap, Stack
see [medium post](https://medium.com/@shoheiyokoyama/understanding-memory-layout-4ef452c2e709)

short answer on stack and heap:

stack: Storing data needed by function calls in a program, **OS kernel** handles the memory allocation, scope **limits to function calls**

heap: Dynamic memory allocation, memory allocation handled by **user**, scope **not limited** variables referenced from several places











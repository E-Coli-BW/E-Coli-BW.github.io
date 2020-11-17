---
layout: post
title:  "大数据杂乱面试问题"
date:   2020-11-16 00:15:07 -0400
tags: big data
categories: [notes]
---

* 大数据框架本身

1. Spark的任务提交模式，每种模式的提交流程是怎样的？

2. 宽窄依赖与Stage划分

    宽依赖：一个parent被多个child使用
    窄依赖：一个parent只被一个child用
    Stage划分主要看宽依赖，因为只要产生了宽依赖，必定有shuffle,有shuffle那就肯定需要进入下一个stage

3. Yarn的调度模式（FIFO， Fair, ?) Fair的调度算法具体是怎样的？

4. Hadoop的任务提交模式

5. Hive: map-side join?

    Map side join is a process where joins between two tables are performed in the Map phase without the involvement of Reduce phase.

    Map-side Joins allows a table to get loaded into memory ensuring a very fast join operation, performed entirely within a mapper and that too without having to use both map and reduce phases.


6. 倒排索引是什么？有什么用？实际的例子？

7. Stage和Task的关系？

    一个stage可以有多个Task

8. Executor, Task, Stage, CPU cores关系是怎样的？

9. 常见的Spark优化方法？
    - 广播大变量供Executor中的Task共享，这样可以省去传大变量的带宽（减少网络IO)
    - 用mapPartition代替map (一次性处理掉partition内所有的数据而不是一个一个处理) 
    - map-side预聚合减少shuffule的总量（e.g:redeuceByKey替代groupByKey)
    - 对多次使用的RDD进行持久化，防止多次重复计算计算图
    - 复用RDD，避免重复建立RDD （理由同上）

10. 脑裂是什么？如何解决?

11. Hadoop和Spark的HA是怎么实现的？

* Java

* NoSQL
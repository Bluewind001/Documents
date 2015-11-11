学习慕课网《Hadoop大数据平台架构与实践--基础篇》教程的笔记
本课程简单的介绍了Hadoop使用和基本工具和工作原理。

[TOC]

## 1-1 课程简介
《Hadoop开发指南》课本。

## 1-2 Hadoop前世今生
Google大数据的技术：MapReduce，BigTable，GFS。

## 1-3 Hadoop功能和优势
__开源+分布式存储+分布式云计算__
__Hadoop开发和运维人才__

## 1-4 Hadoop生态系统和版本
Hive：把SQL翻译成任务
HBase：更高的扩展
zookeeper：监控集群的工具

## 2-1 获取Linux 操作系统
云主机：utask

## 2-2 安装JDK

## 2-3 配置Hadoop
配置4个配置文件，然后格式化。
安装的过程可参考此视频

## 2-4 安装小结

## 3-1 基本概念
块（Block）：
NameNode：是管理节点，存放文件的元数据包括1）文件与数据块的映射表，2）数据块与数据节点的映射表。
DataNode：存放数据块的。
SecondaryNameNode：

## 3-2 数据管理策略
心跳检测：DataNode和NameNode直接的联系，DataNode每隔一定时间会向NameNode报告自己的状况，如网络状态，是否可访问。

## 3-3 HDFS文件读写流程


## 3-4 HDFS特点
1. 数据冗余，硬件容错
2. 流数据访问，一次写入，多次读取。
3. 适合大文件。

## 3-5 HDFS使用
一些命令的使用，如put，get，mkdir， 格式：hadoop fs -ls/-mkdir/get/put

## 4-1 MapReduce原理
>并行计算框架。

分而治之，一个大任务分成多个小的子任务（Map），并行执行后合并返回结果（Reduce）。

## 4-2 MapReduce运行流程
Job&Task：一个Job分成多个Task，Task分成MapTasker和ReduceTasker。
JobTracker：1. 作业调度，2.分配任务，监控任务的执行进度。3. 监控TaskTracker的状态。
TaskTracker：执行任务。

MapReduce容错机制：1）重复执行，如果4次还是失败，就放弃。2）推测执行。

## 5-1,2,3 WordCount单词统计（上，中，下）
这是个利用Hadoop的小例子，可以参考。

## 5-4,5 利用MapReduce进行排序（上，下）

## 5-6 课程总结


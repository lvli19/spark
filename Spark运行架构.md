链接：http://dblab.xmu.edu.cn/blog/1711-2/

# 基本概念
在具体讲解Spark运行架构之前，需要先了解几个重要的概念：
* __RDD__ ：是弹性分布式数据集（Resilient Distributed Dataset）的简称，是分布式内存的一个抽象概念，提供了一种高度受限的共享内存模型；
* DAG：是Directed Acyclic Graph（有向无环图）的简称，反映RDD之间的依赖关系；
* Executor：是运行在工作节点（Worker Node）上的一个进程，负责运行任务，并为应用程序存储数据；
* 应用：用户编写的Spark应用程序；
* 任务：运行在Executor上的工作单元；
* 作业：一个作业包含多个RDD及作用于相应RDD上的各种操作；
* 阶段：是作业的基本调度单位，一个作业会分为多组任务，每组任务被称为“阶段”，或者也被称为“任务集”。

作业 》 阶段 》任务

# 架构设计

Spark运行架构包括 __集群资源管理器（Cluster Manager）、运行作业任务的工作节点（Worker Node）、每个应用的任务控制节点（Driver）和每个工作节点上负责具体任务的执行进程（Executor）__ 。
其中，集群资源管理器可以是Spark自带的资源管理器，也可以是YARN或Mesos等资源管理框架。

与Hadoop MapReduce计算框架相比，Spark所采用的Executor有两个优点：

一是利用 __多线程来执行具体的任务（Hadoop MapReduce采用的是进程模型），减少任务的启动开销；二是Executor中有一个BlockManager存储模块，会将内存和磁盘共同作为存储设备__  ,当需要多轮迭代计算时，
可以将中间结果存储到这个存储模块里，下次需要时，就可以直接读该存储模块里的数据，而不需要读写到HDFS等文件系统里，
因而有效减少了IO开销；或者在交互式查询场景下，预先将表缓存到该存储系统上，从而可以提高读写IO性能。

__总体而言，在Spark中，一个应用（Application）由一个任务控制节点（Driver）和若干个作业（Job）构成，一个作业由多个阶段（Stage）构成，一个阶段由多个任务（Task）组成。__

当执行一个应用时， __任务控制节点__ 会向 __集群管理器（Cluster Manager）申请资源__ ， __启动Executor__ ，并 __向Executor发送应用程序代码和文件，
然后在Executor上执行任务__ ，运行结束后， __执行结果会返回给任务控制节点，或者写到HDFS或者其他数据库中。__ 

# Spark运行基本流程
Spark的基本运行流程如下：

（1）当一个Spark应用被提交时，首先需要为这个应用构建起基本的运行环境，即由任务控制节点（Driver）创建一个SparkContext，由SparkContext负责 __和资源管理器（Cluster Manager）的通信__ 以及 __进行资源的申请、任务的分配和监控等__ 。SparkContext会向资源管理器注册并申请运行Executor的资源；
（2）资源管理器为Executor分配资源，并启动Executor进程，Executor运行情况将随着“心跳”发送到资源管理器上；
（3） __SparkContext根据RDD的依赖关系构建DAG图，DAG图提交给DAG调度器（DAGScheduler）进行解析，将DAG图分解成多个“阶段”（每个阶段都是一个任务集），并且计算出各个阶段之间的依赖关系，然后把一个个“任务集”提交给底层的任务调度器（TaskScheduler）进行处理；__ 
__Executor向SparkContext申请任务，任务调度器将任务分发给Executor运行，同时，SparkContext将应用程序代码发放给Executor；__

（4）任务在Executor上运行， __把执行结果反馈给任务调度器__ ， __然后反馈给DAG调度器__ ， __运行完毕后写入数据并释放所有资源__。

# Spark 安装 http://dblab.xmu.edu.cn/post/5663/



* 来源：子雨大数据 

# 关于Spark
Spark最初由美国加州伯克利大学（UCBerkeley）的AMP（Algorithms, Machines and People）实验室于2009年开发，是基于内存计算的大数据并行计算框架，
可用于构建大型的、低延迟的数据分析应用程序。Spark在诞生之初属于研究性项目，其诸多核心理念均源自学术研究论文。
2013年，Spark加入Apache孵化器项目后，开始获得迅猛的发展，如今已成为 __Apache软件基金会最重要的三大分布式计算系统开源项目之一（即Hadoop、Spark、Storm）__。

Spark作为大数据计算平台的后起之秀，在2014年打破了Hadoop保持的基准排序（Sort Benchmark）纪录，使用206个节点在23分钟的时间里完成了100TB数据的排序，
而Hadoop则是使用2000个节点在72分钟的时间里完成同样数据的排序。也就是说，Spark仅使用了十分之一的计算资源，获得了比Hadoop快3倍的速度。
新纪录的诞生，使得Spark获得多方追捧，也表明了Spark可以作为一个更加快速、高效的大数据计算平台。


__Spark具有如下几个主要特点：__
* __运行速度快__：（从DAG的角度来看）park使用先进的DAG（Directed Acyclic Graph，有向无环图）执行引擎，
以支持循环数据流与内存计算，基于内存的执行速度可比Hadoop MapReduce快上百倍，基于磁盘的执行速度也能快十倍；
* __容易使用__：（从语言的角度来看）
Spark支持使用Scala、Java、Python和R语言进行编程，简洁的API设计有助于用户轻松构建并行程序，并且可以通过Spark Shell进行交互式编程；
* __通用性__：Spark提供了完整而强大的技术栈，包括SQL查询、流式计算、机器学习和图算法组件，__这些组件可以无缝整合在同一个应用中，足以应对复杂的计算__；
* __运行模式多样__：Spark可运行于独立的集群模式中，或者运行于Hadoop中，也可运行于Amazon EC2等云环境中，并且可以访问HDFS、Cassandra、HBase、Hive等多种数据源。

# Spark相对于Hadoop的优势


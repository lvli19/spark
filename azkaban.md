## Spark SQL/Hadoop用于做离线统计处理
ETL
* 1）数据抽取
Sqoop吧RDBMS中的数据抽取到hadoop

Flume进行日志，文本数据的采集，采集到Hadoop

* 2）数据处理

Hive、MapReduce、spark、、、、

* 3）统计结果入库
数据存放到HDFS（Hive、spark SQL、文件）
   
   启动一个Sever：HIveSever2、ThriftServer
   jbdc的方法去访问统计结果
   
   
使用sqoop把结果导出到RDBMS中


这些作业之间是存在时间 __先后依赖关系__ 的
Step A ===>Step B ===> Step C

在没有调度系统的情况

crontab定时调度


- 为了更好的组织起这样复杂执行计算的关系 ==> 这就需要一个工作流调度系统来进行依赖关系作业的调度

Linux crontab +shell
  -- 优点：简答、易用
  -- 缺点：维护


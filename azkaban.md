## Spark SQL/Hadoop用于做离线统计处理（比如ETL
* 1）数据抽取
Sqoop吧RDBMS中的数据抽取到hadoop

Flume进行日志，文本数据的采集，采集到Hadoop

* 2）数据处理

Hive、MapReduce、spark、、、、

* 3）统计结果入库
- 数据存放到HDFS（Hive、spark SQL、文件）
   
   启动一个Sever：HIveSever2、ThriftServer
   jbdc的方法去访问统计结果
   
   
- 使用sqoop把结果导出到RDBMS中


这些作业之间是存在时间 __先后依赖关系__ 的
Step A ===>Step B ===> Step C

- 在没有调度系统的情况

crontab定时调度


- 为了更好的组织起这样复杂执行计算的关系 ==> 这就需要一个工作流调度系统来进行依赖关系作业的调度

Linux crontab +shell

  -- 优点：简答、易用
  
  -- 缺点：维护
         
           依赖（资源利用率比较低（中间的空闲时间）；如果集群在某个时刻压力很大，资源没有申请到；

## 常用的资源调度工具

### Azkaban  轻量级

### Oozie
  重量级
  
  cm hue
  xml
### 宙斯（Zeus)

## Azkaban概述

* Open-source Workflow Manager
* 批处理工作流，用于跑hadoop的job
* 提供了一个易于使用的用户界面来维护和跟踪你的工作流程

插入图片 https://azkaban.github.io/

### 特性 https://azkaban.readthedocs.io/en/latest/

* 与各个版本的hadoop兼容
* 易于使用webui
* Simple web and http workflow uploads 方便上传工作流
* Project workspaces 方便设置任务之间的关系
* Scheduling of workflows 工作流调度
* Modular and pluginable 模块化和可插拔的
* Authentication and Authorization  可以根据权限登陆的
* Tracking of user actions 可以跟踪操作行为
* Email alerts on failure and successes email告警
* SLA alerting and auto killing SLA告警和自动杀掉
* Retrying of failed jobs  失败作业的重试

### Azkaban的架构
* 1、Relational Database(Mysql)
azkaban将大多数状态信息都存于MySQL中,Azkaban Web Server 和 Azkaban Executor Server也需要访问DB。
* 2、Azkaban Web Server
提供了Web UI，是azkaban的主要管理者，包括 project 的管理，认证，调度，对工作流执行过程的监控等。

* 3、Azkaban Executor Server

调度工作流和任务，纪录工作流活任务的日志，之所以将AzkabanWebServer和AzkabanExecutorServer分开，主要是因为在某个任务流失败后，可以更方便的将重新执行。而且也更有利于Azkaban系统的升级


### azkaban的工作模式

* the stand alone “solo-server” mode 
     信息存储在H2 ===>mysql
     webserver和execserver是运行在一个进程中
* distributed multiple-executor mode. 
   存储在MySQL中
   运行在不同的hosts中
   
   



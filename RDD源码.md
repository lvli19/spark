
# RDD 五大特性 
* Internally, each RDD is characterized by five main properties:

 - A list of partitions
 
 - A function for computing each split
 
 - A list of dependencies on other RDDs

 - Optionally, a Partitioner for key-value RDDs (e.g. to say that the RDD is hash-partitioned)

 - Optionally, a list of preferred locations to compute each split on (e.g. block locations for an HDFS file)

# RDD五大特性的源码体现

```
def compute(split: Partition, context: TaskContext): Iterator[T] //特性二，计算
  
protected def getPartitions: Array[Partition] //特性一，一堆的partitions
  
protected def getDependencies: Seq[Dependency[_]] = deps //特性三，依赖关系

protected def getPreferredLocations(split: Partition): Seq[String] = Nil //特性五，优先位置

@transient val partitioner: Option[Partitioner] = None
```
## SparkContext SparkConf ##  
首先需要创建 SparkContext
 链接到Spark集群-----local standalone yarn mesos
 通过SparkContext来创建RDD，广播变量到集群

在创建SparkContext之前还需要创建SparkConf对象

Some notes on reading files with Spark:

* If using a path on the local filesystem, the file must also be accessible at the same path on worker nodes. Either copy the file to all workers or use a __network-mounted shared file system.__ 

* All of Spark’s file-based input methods, including textFile, support running on directories, compressed files, and wildcards as well. For example, you can use textFile("/my/directory"), textFile("/my/directory/*.txt"), and textFile("/my/directory/*.gz").

* The textFile method also takes an optional second argument for controlling the number of partitions of the file. By default, Spark creates one partition for each block of the file (blocks being 128MB by default in HDFS), but you can also ask for a higher number of partitions by passing a larger value. Note that you cannot have fewer partitions than blocks.

### 创建RDD的两个方式
* parallel collections
* External Datasets

## 开发pyspark应用程序
* IDE：IDEA pycharm
* 设置基本参数： python interceptor PYTHONPATH SPARK_HOME 2zip包
* 开发
* 使用local进行本地化测试

## 提交pyspark应用程序
./spark-submit --master local[2] --name spark0301 /home/hadoop/script/spark0301.py



 


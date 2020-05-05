
# RDD 五大特性 
* Internally, each RDD is characterized by five main properties:

 - A list of partitions
 
 - A function for computing each split
 
 - A list of dependencies on other RDDs

 - Optionally, a Partitioner for key-value RDDs (e.g. to say that the RDD is hash-partitioned)

 - Optionally, a list of preferred locations to compute each split on (e.g. block locations for an HDFS file)

# RDD五大特性的源码体现

```
  def compute(split: Partition, context: TaskContext): Iterator[T]
```

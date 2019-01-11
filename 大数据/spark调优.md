##Spark性能调优

###1.数据序列化
	1.kyro序列化
	val conf = new SparkConf().setMaster(...).setAppName(...)
    conf.set("spark.serializer","org.apache.spark.serializer.KryoSerializer")
	conf.registerKryoClasses(Array(classOf[MyClass1], classOf[MyClass2]))
	val sc = new SparkContext(conf)
	
	
###2.内存调优
	
	
	
	
####3.streaming调优
	1.streaming batch时间选择
	对于批处理时间和窗口大小的设定，并没有统一的标准。通常是先从一个比较大的批处理时间
	（10秒左右）开始，然后不断地使用更小的值进行对比测试。如果Spark Streaming用户界面中
	显示的处理时间保持不变，则可以进一步设定更小的值；如果时间开始增加，则可能已经达到了应
	用的极限，再减小该值则可能会影响系统的性能。
	2.使用高效算子
		1）reduceByKey会在Map端做本地聚合，使得Shuffle过程更加平缓，而groupByKey等 Shuffle操作不会在Map端做聚合。因此能使用reduceByKey的地方尽量使用该算子，避
	免出现groupByKey().map(x=>(x._1,x._2.size))这类实现方式。
		2）mapPartition foreachPartition
	
	3.数据倾斜
		当数据发生倾斜(某一部分数据量特别大)，虽然没有GC(Garbage Collection，垃圾 回收)，但是task执行时间严重不一致。 需要重新设计key，以更小粒度的key使得task大小合理化。 l 修改并行度。
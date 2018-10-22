#scala笔记
##一、基础概念
###1.占位符
<p>	为了让函数字面量更加简洁，我们可以使用下划线作为一个或多个参数的占位符，只要每个参数在函数字面量内仅出现一次。</p>
	scala> val numList = List(-3, -5, 1, 6, 9)
	numList: List[Int] = List(-3, -5, 1, 6, 9)
	scala> numList.filter(x => x > 0 )
	res1: List[Int] = List(1, 6, 9)
	scala> numList.filter(_ > 0)
	res2: List[Int] = List(1, 6, 9)

###2.对象 object
	使用场景：
	1.任何在java或者C++使用单例对象的地方
	2.存放工具函数或者常量的地方
	2.需要单个实例来协调某个服务（参考单例模式）
	







##二、疑惑点
###1.private[this]
	表示该字段 不生成getter或setter


表示关系的UML标记
==================================================

>旧博客备份 2011-03-07 http://www.blogbus.com/addcn-logs/108043959.html



## 前言
《设计模式解析》读书笔记

——表示关系的UML标记

表示关系的UML标记有如下四种：

1、聚类 （A聚合了B，B是A的一部分）

2、组合 （A是由B组成的，A包含B菱形的对象）

3、继承 （B攀升自A，A泛化了B）

4、依赖 （A依赖于B，A使用B）

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/design-patterns-explained-uml-1.png)

1、is-a关系

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/design-patterns-explained-uml-2.png)
 
图2-2中，Shap类下面的箭头的意思是，指向Shape的那些类派生自Shape类。

2、has-a关系

有两种不同的has-a关系。一个对象可以拥有另一个对象，其中被包含的对象是包含对象的一部分——或者不是。

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/design-patterns-explained-uml-3.png)


图2-3中，表示出Airport“拥有”Aircraft。Aircraft并不是Airport的一部分，但仍然可以说Airport拥有aircraft，这种关系成为聚类 。
此外，图中还表示了Aircraft要么是Jet（喷气式飞机），要么是Helicopter（直升飞机）。也就是说，Airport可以拥有Jet或Helicopter，但它是以相同方式对待他们的（当作Aircraft）。Airport类右边是空心的（未填充的）菱形表示聚类关系。

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/design-patterns-explained-uml-4.png)


另一种has-a关系是包含，被包含对象是包含对象的一部分，这种关系也称为组合 。

图2-4现实了Car（轿车）拥有Tire（轮胎），后者是它的一部分（也就是说，Car有Tire和其他东西组成），这种has-a关系，称为组合关系（composition），用实心菱形表示。此图上还显示了Car使用了GasStation（加油站）类，这种使用关系用带箭头的虚线表示，也称依赖关系（dependcncy relationship）。

组合和聚类都有“一个对象包含一个或多个对象”的意思，但是，组合意味着“被包含对象是包含对象的一部分”，而聚类意味着被包含对象更像是一个集合。我们可以认为组合是一种非共享的关联，被包含对象的生存周期由包含对象控制。

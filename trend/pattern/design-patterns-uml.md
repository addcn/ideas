UML类图
==================================================

《大话设计模式》读书笔记

UML类图中的基本图示法：

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple.jpg)


### 1、类图

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-class.jpg)

矩形框，代表一个类（Class）。类图分三层，第一层显示类的名称，如果是抽象类，则用*斜体*显示。第二层是类的特性，通常就是字段和属性。第三层是类的操作，通常是方法或行为。注意前面的符号‘+’鄙视public，‘-’表示priate，‘#’表示protected。

### 2、接口图

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-interface.jpg)

与类图的主要区别是顶端有<<interface>>显示。

第一行是接口名称，第二行是接口方法。接口还有另一种表示方法，俗称棒棒糖表示法。


### 3、关系表示

#### 3.1 继承关系

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-rel-inherit.jpg)

继承关系用**空心三角形+实线**来表示。


#### 3.2 接口关系

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-rel-interface.jpg)

实现接口用**空心三角形+虚线**来表示。


#### 3.3 关联关系（association）

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-rel-association.jpg)

关联关系用**实线箭头**来表示。




#### 3.4 聚合关系（aggregation）

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-rel-aggregation.jpg)

聚合关系用**空心菱形+实线箭头**来表示。


#### 3.5 合成/组合关系（composition）

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-rel-composition.jpg)

合成关系用**实心菱形+实线箭头**来表示。

另外，合成关系的连线两端还有一个数字‘1’和数字‘2’，这被称为基数。表明这一端的类可以有几个实例，如果一个类可能有无数个实例，则用'n'来表示。

关联关系、聚合关系也可以有基数的。


#### 3.6 依赖关系（dependency）

![image](https://raw.githubusercontent.com/addcn/ideas/master/statics/upload/patterns/uml-exmaple-rel-dependency.jpg)

依赖关系用**虚线箭头**表示。


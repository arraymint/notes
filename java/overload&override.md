# 重载&重写

## 定义上的区别：

1、重载是指不同的函数使用相同的函数名，但是函数的参数个数或类型不同。调用的时候根据函数的参数来区别不同的函数。

2、覆盖（也叫重写）是指在派生类中重新对基类制中的虚函数（注意是虚函数）重新实现。即函数名和参数都一样，只是函数的实现体不一样。

二、规则上的不同：

1、重载的规则：

- 必须具有不同的参数列表。
- 可以有不同的访问修饰符。
- 可以抛出百不同的异常。

2、重写方法度的规则：

①参数列表必须完全与被重写的方法相同，否则不能称其为重写而是重载。

②返回的类型必须一知直与被重写的方法的返回类型相同，否则不能称其为重写而是重载。

③访问修饰符的限制一定要大于被重写方法的访问修饰符。

④重写方法一定不能抛出新的检查异常或者比被重写方法申明更加宽泛的检查型异常。

三、类的关道系上的区别：

重写是子类和父类之间的关系，是垂直关系；重载是同一个类中方法之间的关系，是水平关系。
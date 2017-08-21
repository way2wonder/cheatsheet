 ### Item 13: Minimize the accessibility of classes and members
> api 和  实现部分分离


1. 拇指原则: make each class or member as inaccessible as possible
2. 如果`package-private top-level class`只被一个类所用,那么可以把他作为一个私有的内部类使用,减少公共类的可见性更重要

作为成员属性
  + fields
  + methods
  + nested classes
  + nested interfaces
他们有4种可能的可见等级
  + private
  + package-private
  + protected
  + public

包含有可变域的类并不是线程安全的.
同样适用于静态域.  如果静态域所引用的对象可以被修改,会导致灾难性的后果.
长度不为0的数组总是可变的
1. 将数组变成私有,然后返回个公有的List
2. 将数组变成私有,然后通过公共方法返回这个数组

### Item 14: In public classes, use accessor methods, not public fields
公有类中提供公共的方法来提供私有域的访问.
但如果类是`包级私有的,或者私有的嵌套类`,那么直接访问数据域反而更直观


### Item 15: Minimize mutability(最小化可变性)
将一个类变成不可变遵循以下5个原则
1. 不提供任何修改对象状态的方法  mutator
2. 保证类不会被扩展  
    + final类
    + 将构造器变成私有或者包级私有,然后通过静态工厂方法来返回对象的实例  
3. 是所有的域都是final
4. 将所有域变成private
5. Ensure exclusive access to any mutable components. 如果有指向可变对象的域,要确保客户端无法获得指向这些对象的引用
   + 不用客户端提供的对象初始化这样的域
   + 也不从任何accessor中返回该对象的引用
   + 在构造器和访问方法中用保护性拷贝(defensive copy)技术

不可变对象的几个特点
- 不可变类本质上是线程安全的,他们不要求同步.
所以不可变对象是自由共享的.
- 不仅可以共享不可变对象,甚至可以共享他们的内部信息. 比如: `BigInteger.negate()`
- 不可变对象是其他对象的重要构建块
- 不可变对象唯一缺点就是对应不同的值需要有单独的对象 比如`BigInteger和BitSet`的不同,BitSet是可变的



### Item 16: Favor composition over inheritance 组合优于继承
包装类几乎没有什么缺点,就是不适合在 **`回调框架`** 中使用
>The disadvantages of wrapper classes are few. One caveat is that wrapper
classes are not suited for use in callback frameworks, wherein objects pass selfreferences to other objects for subsequent invocations (“callbacks”). Because a
wrapped object doesn’t know of its wrapper, it passes a reference to itself (this)
and callbacks elude the wrapper.

判断方法  `is-a`   or  `has-a`


### Item 17: Design and document for inheritance or else prohibit it.  为继承设计和写文档,不然就禁用继承

无论是clone 还是 readObject ,都不可以调用可覆盖的方法,不管是直接还是间接的.
+ **In the case of the readObject method, the overriding method will run before the subclass’s state has been deserialized.**
+ **In the case of the clone method, the overriding method will run before the subclass’s clone method has a chance to fix the clone’s state.**

> + to ensure that the class never invokes any of its overridable methods and to document this fact.
+ 通过机械的方法除去它调用自身调用覆盖方法. 将override方法体全部复制到一个helper方法中,自身覆盖的时候调用helper方法,不调用override方法


### Item 18: Prefer interfaces to abstract classes 接口优于抽象方法
java提供两种机制定义一个类型:
   + 抽象类
   + 接口

+ Existing classes can be easily retrofitted(花式翻新) to implement a new interface
+ Interfaces are ideal for defining mixins.
+ 接口允许我们构建非层次结构的framework.  Singer Writer
+ Interfaces enable safe, powerful functionality enhancements via the wrapper class idiom 通过包装类能提供安全有力的增强效果.
可以结合接口和抽象类的优势,整合个骨架类出来.
比如:  AbstractCollection AbstractSet  **自己实现个List**

其实就是包装模式.  wrapper
The class implementing the interface can forward invocations of interface methods to a
contained instance of a private inner class that extends the skeletal implementation.

### Item 19: Use interfaces only to define types
 It is inappropriate to define an interface for any other purpose. 不能滥用接口
 + The constant interface pattern is a poor use of interfaces. `constant interface`  这就是个失败的用法.
 如果你想export Constants, 有几种选择.
 + 如果常量和类或者接口紧耦合,那么就将他们加入到类中. 比如Integer MIN_VALUE
 + Enum  type
 + 用一个不能实例化的工具类 (**如果经常用的话,可以用`static import`这样就不用输入很多的类名啦**)

 In summary, interfaces should be used only to define types. They should not
 be used to export constants.

### Item 20: Prefer class hierarchies to **`tagged classes`**
tagged classes are verbose(冗长), error-prone(易出错的), and inefficient.

 ```java
 // Tagged class - vastly inferior to a class hierarchy!
class Figure
{
    enum Shape
    {
        RECTANGLE, CIRCLE
    }

    ;
    // Tag field - the shape of this figure
    final Shape shape;
    // These fields are used only if shape is RECTANGLE
    double length;
    double width;
    // This field is used only if shape is CIRCLE
    double radius;

    // Constructor for circle
    Figure(double radius)
    {
        shape = Shape.CIRCLE;
        this.radius = radius;
    }

    // Constructor for rectangle
    Figure(double length, double width)
    {
        shape = Shape.RECTANGLE;
        this.length = length;
        this.width = width;
    }

    double area()
    {
        switch (shape)
        {
            case RECTANGLE:
                return length * width;
            case CIRCLE:
                return Math.PI * (radius * radius);
            default:
                throw new AssertionError();
        }
    }
}
 ```


### Item 21: Use function objects to represent strategies  (Comparator就是这个的最好证明)
什么是`function objects`?(例如实现Compartor接口的类就算是一个function Objects)
>it is possible to define an object whose methods perform operations on other objects, passed explicitly to the methods.An instance of a class that exports exactly one such method is effectively a pointer to that method. Such instances are known as function objects.
因为`StringLengthComparator`没有field,所以他是没状态的,所以可以用单例模式返回一个实例.



### Item 22: Favor static member classes over nonstatic   静态成员类优于非静态的
nested classes:
+ static member classes
+ nonstatic member classes
+ anonymous classes
+ local classes
除了第一个,其他的都是`inner classes` 内部类

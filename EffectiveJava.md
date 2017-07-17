# creating and destroying Objects

### Consider static factory methods instead of constructors (静态方法优于构造方法)

  - 优点：

    1. One advantage of static factory methods is that, unlike constructors, they have names.(静态方法有名字)
    2. unlike constructors,they are not required to create a new object each time they're invoked （ `immutable classes`例子:`Boolean.valueOf` )

      - similar to `Flyweight pattern`
      - Classes that do this are said to be `instance-controlled`
      - 被调用的时候不用每次都实例化一个对象
      - `instance-controlled` 可以确保使用`==`比较,而不需要用`equals`比较,这样能提高性能

    3. they can return an object of any subtype of their return type (可以返回子类型)

      - 可以不用让类public
      - 接口不能有静态方法,所以静态工厂方法对于接口类型Type 被放到了不能实例化的类Types里面,ex:`Collection Collections`
      - 不仅返回的类可以不是public class,而且返回的类的实现也可以根据每次调用的时候参数值的不同而改变 ex:`EnumSet RegularEnumSet JumboEnumSet`
      - `service provider frameworks` ex: `JDBC` 多种service的实现,将多种实现暴露给客户端,实现与实现间解耦.

        1. `a service interface` , which providers implement
        2. `a provider registration API`, which the system uses to register implementations, giving clients access to them;
        3. `a service access API`, which clients use to obtain an instance of the service.
        4. `a service provider interface`,which providers implement to create instances of their service implementation. (optional)
        5. > In the case of JDBC,

          > - Connection plays the part of the service interface,
          > - DriverManager.registerDriver is the provider registration API,
          > - DriverManager.getConnection is the service access API,
          > - and Driver is the service provider interface.

    4. they reduce the verbosity(冗长的) of creating parameterized type instances。(减少创建实例时输入的参数)

      > ```java
      >    public static <K, V> HashMap<K, V> newInstance()
      >    {
      >        return new HashMap<K, V>();
      >    }  
      >    Map<String, List<String>> m = HashMap.newInstance();
      > ```

  - 缺点：

    - 主要的缺点就是 不是public或者protected的类不能转化成subClass（子类)

      - public工厂方法返回的 nonpublic classes 也是不能转化成子类的

    - 不容易从其他的静态方法中区分出来

  - 总结

    - In summary, static factory methods and public constructors both have their uses, and it pays to understand their relative merits. Often static factories are preferable, so avoid the reflex to provide public constructors without first considering static factories.
    - 静态工厂方法和构造器都有各自的用途,理解他们的相对有点是值得的. 一般静态优于构造方法,所以一般第一反应是构造方法而不是构造方法

### Consider a builder when faced with many constructor parameters(面对多个构造参数的时候选择Builder)
```java
private final int servingSize; // (mL) required
private final int servings; // (per container) required
private final int calories; // optional
private final int fat; // (g) optional
private final int sodium; // (mg) optional
private final int carbohydrate; // (g) optional
```
有以下几种方法
1. telescoping constructor  重叠构造方法.  太冗余啦  
   +  the telescoping constructor pattern works, but it is hard to write
   client code when there are many parameters,
   + and harder still to read it.
2. JavaBean
   + a JavaBean may be in an inconsistent state partway through its construction. 构造过程中可能状态不一致
   + JavaBeans pattern precludes the possibility of making a class immutable JavaBean模式排除了创建一个不变的类的可能,需要额外的努力使得线程安全
3. Builder
  - 优点:
    + Methods that take a Builder instance would typically constrain the builder’s
type parameter using a bounded wildcard type (Item 28)
    + The traditional Abstract Factory implementation :`Class`类
       +  `Class.newInstance` breaks compile-time exception checking. The Builder interface,corrects these deficiencies(不足).
  - 缺点:
    + 创建bean 就必须创建builder. 微小的性能消耗
    + 相对于覆盖构造法显得稍微冗余
4. 总结:
In summary, the Builder pattern is a good choice when designing classes
whose constructors or static factories would have more than a handful of
parameters
如果参数个数超过1只手,Builder 模式就是个很好的选择

### Enforce the singleton property with a private constructor or an enum type. 强制单例的属性拥一个私有的构造方法或者是个枚举类型

1. Making a class a singleton can make it difficult to test its clients 单例模式使得测试他的客户端变难了
2. 

## 服务提供者框架

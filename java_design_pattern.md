## Creational 构造模式

1. Abstract Factory
2. Adapter






### Abstract Factory

**使用场景：**

- a system should be independent of how its products are created, composed and represented  （系统必须将产品的创建，组成和展现分离）
- a system should be configured with one of multiple families of products  （系统由相似的产品组成）
- a family of related product objects is designed to be used together, and you need to enforce this constraint(相关的对象需要用在一起，而你又需要强制这种约束)
- you want to provide a class library of products, and you want to reveal（显示，揭露） just their interfaces, not their implementations

![抽象工程模式UML图](./pictures/abstract-factory_1.png)


### Adapter
**使用场景：**

- you want to use an existing class, and its interface does not match the one you need（你想使用一个已经存在的类，但是他的接口和你需要的不匹配）
- you want to create a reusable class that cooperates with unrelated or unforeseen classes, that is, classes that don't necessarily have compatible interfaces
- you need to use several existing subclasses, but it's impractical to adapt their interface by subclassing every one. An object adapter can adapt the interface of its parent class. （***<font color="red">这里我暂时还不清楚</font>***）

![Adapter](./pictures/adapter.png)



### Builder

**使用场景：**

* the algorithm for creating a complex object should be independent of the parts that make up the object and how they're assembled  （构造分离）
* the construction process must allow different representations for the object that's constructed（构造器必须允许对象的不同表现形式）
![Builder](./pictures/builder_1.png)



### Multiton  （多例，又叫Registry）
**使用场景：**

* Ensure a class only has limited number of instances, and provide a global point of access to them.（确保一个类只有有限的实例，切需要提供一个全局的入口用于获取他们）

![Builder](./pictures/multiton.png)


```java
  static {
    nazguls = new ConcurrentHashMap<>();
    nazguls.put(NazgulName.KHAMUL, new Nazgul(NazgulName.KHAMUL));
    nazguls.put(NazgulName.MURAZOR, new Nazgul(NazgulName.MURAZOR));
    nazguls.put(NazgulName.DWAR, new Nazgul(NazgulName.DWAR));
    nazguls.put(NazgulName.JI_INDUR, new Nazgul(NazgulName.JI_INDUR));
    nazguls.put(NazgulName.AKHORAHIL, new Nazgul(NazgulName.AKHORAHIL));
    nazguls.put(NazgulName.HOARMURATH, new Nazgul(NazgulName.HOARMURATH));
    nazguls.put(NazgulName.ADUNAPHEL, new Nazgul(NazgulName.ADUNAPHEL));
    nazguls.put(NazgulName.REN, new Nazgul(NazgulName.REN));
    nazguls.put(NazgulName.UVATHA, new Nazgul(NazgulName.UVATHA));
  }

  private Nazgul(NazgulName name) {
    this.name = name;
  }

  public static Nazgul getInstance(NazgulName name) {
    return nazguls.get(name);
  }
```
  
代码中 `getInstance `中用的是map获取对象实例的，而不是用得new，这样的好处就是不用每次都去new一个实例。




# Twin

**使用场景：**  
* Twin pattern is a design pattern which provides a standard solution to simulate multiple inheritance in java（实现多重继承的一种设计模式，java原本是不支持多重继承的）


---
这3个设计模式没包含在difficulty里面

* Aggregator Microservices
* Message Channel
* Publish Subscribe  


## CallBack  


![CallBack 设计模式](./pictures/callback.png)

>jdk中的`CyclicBarrier` 
	

## DAO （Data Access Object）
![](./pictures/dao.png)



## Data  Mapper
![](./pictures/data-mapper.png)


##  Decorator（Wrapper 装饰模式，或者叫包装模式）
>  EX: `JDK中得IO流`  
>  这里可以将IO流彻底的复习一下，顺便掌握一下NIO

**使用场景：**

* to add responsibilities to individual objects dynamically and transparently, that is, without affecting other objects
* for responsibilities that can be withdrawn（撤离）
* when extension by subclassing is impractical.（用子类扩展不现实） Sometimes a large number of independent extensions are possible and would produce an explosion of subclasses to support every combination. Or a class definition may be hidden or otherwise unavailable for subclassing（类定义被隐藏或者不能实现子类）

JDK IO：
![](./pictures/java_io.png)




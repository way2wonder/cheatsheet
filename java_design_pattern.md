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

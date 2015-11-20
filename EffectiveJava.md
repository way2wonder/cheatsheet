

###  creating and destroying  Objects
1. Consider static factory methods instead of constructors
 
    + 优点：
        - One advantage of static factory methods is that, unlike constructors, they have names.(静态方法有名字)
        - unlike constructors,they are not required to create a new object each time they’re invoked  （similar to Flyweight pattern）
        - they can return an object of any subtype of their return type  (可以返回子类型的实例)
        - they reduce the verbosity of creating parameterized type instances。
    + 缺点：
        - 主要的缺点就是 不是public或者protected的类不能转化成subClass（子类

        - 不容易从其他的静态方法中区分出来
```java
public static <K, V> HashMap<K, V> newInstance()
{
    return new HashMap<K, V>(); 
}  
Map<String, List<String>> m = HashMap.newInstance(); 

```

减少了参数的书写


##服务提供者框架


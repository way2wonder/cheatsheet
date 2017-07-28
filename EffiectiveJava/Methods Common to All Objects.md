### Item 8: Obey the general contract when overriding equals (复写`equals`方法)
满足一下任意条件都不需要重写`equals`方法
   1. Each instance of the class is inherently unique . 类的每个实例本质上都是唯一的
   2. You don’t care whether the class provides a “logical equality” test 客户端不关心或者不使用 `equals`方法
   3. A superclass has already overridden equals, and the superclass behavior is appropriate for this class. 超类已经重新啦`equals`方法,且对于这个类也是适合的.
   4. The class is private or package-private, and you are certain that its equals method will never be invoked. 这种情况下无疑是需要重新equals方法的,以防止equals方法被调用

什么时候需要重写呢?
>如果类具体自己的`逻辑相等` 比如`Integer`或者`Date`,而超类没有覆盖`equals`方法以实现期望的行为,这时候就需要重写`equals`方法. 这样做也使得类的实例可以作为Map的key值,或者Set的元素

**a class that uses instance control (Item 1) to ensure that at most one object exists with each value.** 比如Enum类型. 逻辑相等等同于类相等


重写`equals`方法需要满足一下几个特性:
  1. Reflexive 自反性  及非null引用, 本身equals本身
  2. Symmetric 对称性  x.equals(y)  y.equals(x)
  3. Transitive 传递性  x.euals(y)  y.equals(z) then  x.equals(z)
  4. For any non-null reference value x, x.equals(null) must return false  非空和空比较始终返回false
  5. Consistent 一致性  多次调用始终返回true或者false

重写`equals`方法的几个诀窍
 1. Use the == operator to check if the argument is a reference to this object
 2. Use the instanceof operator to check if the argument has the correct type  (包括参数null判断)
 3. Cast the argument to the correct type. 强制转化成正确的类型
 4. 检测参数的域是否和当前对象对应的域是否相匹配
     + 非float和double类型的原生类型直接 ==
     + float 用`Float.compare`,double 用`Double.compare`
     + 引用类型,递归使用equals方法

`(field == null ? o.field == null : field.equals(o.field))`

This alternative may be faster if field and o.field are often identical:

`(field == o.field || (field != null && field.equals(o.field)))`
比较的时候先比较低开销的域,再比较多开销的域,通过域的范式(canonical form)进行比较可以低开销的精确比较

**注意:**
  1. Always override hashCode when you override equals
  2. Don’t try to be too clever. 比如不要想让File的 symbolic links 指向同一个文件就认为两个File对象相等
  3. Don’t substitute another type for Object in the equals declaration.   equals(Object o) `Object`不要换成其他类型


### Item 9: Always override hashCode when you override equals
Object约定
1. hasCode始终返回同一个整数如果equals比较所用到的信息没有改变的话
2. 如果两个对象equals ,那么他们的hashCode也是一样的
3. 如果两个对象不equals,那么他们的hashCode不一定要不同,但最好是不同,因为这样可以提高hash列表的性能

生成hashCode的方法
1. 把某个非零的常数值保存名为result的int类型中
2. 对象中的每个关键域field(f)
   + a为域计算int类型的散列码
     - boolean    f?1:0
     - byte/char/short/int  (int)f
     - long   (int)(f^(f>>>32))   **这里`f>>>32`啥意思**
     - float  Float.floatToIntBits(f)
     - Double  Double.doubleToLongBit(f) 然后按照long的类型得到
     - 如果是引用类型,那么递归调用hashCode方法,如果为null,返回0
     - 如果是个数组,那么就按照2.b的方法将每个数组元素组合下或者用Arrays.hashCode方法
  + b result = 31*result+c; c为2.a得到的int值   
  >`31 * i == (i << 5) - i`

3. 返回result即为hashCode
4. 确认相等的实例有相等的hashCode

>Do not be tempted to exclude significant parts of an object from the hash code computation to improve performance. 不要试图排除对象的重要域来提高生成hashCode的性能



### Item 10: Always override toString
1. providing a good toString implementation makes your class
much more pleasant to use.
2. When practical, the toString method should return all of the interesting information contained in the object

### Item 11: Override clone judiciously 谨慎的覆盖clone方法
1. x.clone() != x  总是true
2. x.clone().getClass() == x.getClass()  true
3. x.clone().equals(x) true    但都不是绝对条件
Clone 创建一个类的实例而不调用构造方法.(太强硬啦 行为良好的clone方法可以调用构造器,然后再复制数据)

if you override the clone method in a nonfinal class, you should
return an object obtained by invoking super.clone

In practice, a class that implements Cloneable is expected to provide a properly functioning public clone method. 实现了Cloneable方法,那么就提供一个功能良好的公共克隆方法

clone 有很多缺点,所以一般专家级的程序员都不复写clone方法
通过拷贝构造器或者拷贝工厂提供clone方法的功能
  + 不依赖有风险的,语言之外的对象创建机制
  + 不要求遵守尚未制定好的文档规范
  + 不会和final域的正常使用发生冲突
  + 不会抛出不必要的受检异常
  + 不需要进行类型转换

### Item 12: Consider implementing Comparable 考虑实现Comparable接口
1. 自反性    must ensure sgn(x.compareTo(y)) == -sgn(y.compareTo(x)) for all x and y
2. 传递性   `(x.compareTo(y) > 0 && y.compareTo(z) > 0) implies x.compareTo(z) > 0.`
3. 分配率   x.compareTo(y) == 0 implies that sgn(x.compareTo(z)) == sgn(y.compareTo(z)), for all z.
4. It is strongly recommended, but not strictly required, that (x.compareTo(y)
== 0) == (x.equals(y)).  如果不满足这点需要特别说明下
> BigDecimal  hashSet  
> BigDecimal TreeSet
> add new BigDecimal("1.0") and new BigDecimal("1.00")
> hashSet 两个元素  TreeSet 一个元素   ,hashSet用的是equals  TreeSet用的是compareTo

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

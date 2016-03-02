1.  多线程安全的前提他是单线程安全

stateless: it has no fields and references no fields from other classes.
无状态的即为：没有全局变量或者其他类的句柄

Stateless objects are always thread-safe.




2. Atomicity 原子性
    Race Conditions：竞争条件
    java.util.concurrent.atomic 中提供原子性的相关java类
3. Locking 锁
     Intrinsic Locks  固有的锁
     Reentrancy means that locks are acquired on a per-thread rather than per-invocation basis.  重进入针对于每个线程，而不是针对每次调用

     ReentrantLock  java5 中的新类，可以研究一番

     4个好处：
      + Polled and Timed Lock Acquisition 
      + Interruptible Lock Acquisition  中断的获取锁请求
      + Non-block Structured Locking  非块结构的锁
      + Fairness   公平
  
     Every shared, mutable variable should be guarded by exactly one lock. Make it clear to maintainers which lock that is.
    每个共享的可变的变量都应该通过锁以确保维护者知道是那个锁

    一般都把共享的变量封装在一个类里面，比如Vector类，但是这样是不好的，往类里面加个方法或者变量就很容易颠覆他的锁机制


    using two different synchronization mechanisms would be confusing and would offer no performance or safety benefit.
    最好不要试用两种同步机制，以防止混淆

    There is frequently a tension between simplicity and performance. When implementing a synchronization policy, resist the temptation to prematurely sacriflce simplicity (potentially compromising safety) for the sake of performance.
     
     简单和性能之间关系略紧张，抵制贸然地牺牲简单性来满足性能需求

     Avoid holding locks during lengthy computations or operations at risk of not completing quickly such as network or console I/O.
     长计算或者网络计算或者IO交互的时候（不能很快的计算完的操作）  避免占有锁

4. Sharing Objects
    + Stale data  不新鲜的数据
    + Nonatomic 64-bit Operations 64位操作不是原子性的
    + 锁和可见性
    + Volatile Variables 易变的，不稳定的数据 
    
    Locking is not just about mutual exclusion; it is also about memory visibility. To ensure that all threads see the most up-to-date values of shared mutable variables, the reading and writing threads must synchronize on a common lock.
    读线程和写线程必须公用一个共同的锁才能保证他们看到的数据是最新的


    Volatile variables are convenient, but they have limitations. The most common use for volatile variables is as a completion, interruption, or status flag, such as the asleep flag in Listing 3.4
    volatile 变量有局限性，一般只用于完成，中断，或者状态标志

    Locking can guarantee both visibility and atomicity; volatile variables can only guarantee visibility.
    锁能保证可见性和原子性，而 volatile只能保证可见性
    

    以下三种情景可以使用volatile关键字

    + Writes to the variable do not depend on its current value, or you can ensure that only a single thread ever updates the value;
    变量的读写不依赖于当前的值

    + The variable does not participate in invariants with other state variables;

    + Locking is not required for any other reason while the variable is being accessed.  变量被触及的时候不需要锁

    
    Publication and Escape  发布和逸出

    Thread confinement
    说明：Thread confinement is the practice of ensuring that data is only accessible from one thread. Such data is called thread-local as it is local, or specific, to a single thread.


     1.  ad-hoc  thread confinement
     2.  stack thread confinement
     3.  ThreadLocal  对象

     不可变性 一个不可变对象要满足以下三点
     An object is immutable if:

        Its state cannot be modifled after construction;

        All its flelds are final;[12] and

        It is properly constructed (the this reference does not escape during construction).


    this逸出 详解：
    this逃逸
是指在构造函数返回之前其他线程就持有该对象的引用. 调用尚未构造完全的对象的方法可能引发令人疑惑的错误, 因此应该避免this逃逸的发生.
this逃逸经常发生在构造函数中启动线程或注册监听器时, 如:
```java
public class ThisEscape {  
    public ThisEscape() {  
        new Thread(new EscapeRunnable()).start();  
        // ...  
    }  
      
    private class EscapeRunnable implements Runnable {  
        @Override  
        public void run() {  
            // 通过ThisEscape.this就可以引用外围类对象, 但是此时外围类对象可能还没有构造完成, 即发生了外围类的this引用的逃逸  
        }  
    }  
}  
```
 在构造函数中创建Thread对象是没有问题的, 但是不要启动Thread. 可以提供一个init方法, 如:

```java
public class ThisEscape {  
    private Thread t;  
    public ThisEscape() {  
        t = new Thread(new EscapeRunnable());  
        // ...  
    }  
      
    public void init() {  
        t.start();  
    }  
      
    private class EscapeRunnable implements Runnable {  
        @Override  
        public void run() {  
            // 通过ThisEscape.this就可以引用外围类对象, 此时可以保证外围类对象已经构造完成  
        }  
    }  
}  
```




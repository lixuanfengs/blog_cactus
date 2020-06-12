---
title: JavaEE面试题
date: 2020-06-12 10:14:38
tags: 面试题
categories: 面试题
toc: true
author: 仙人球
---

## 3. Java SE

## 3.1 你是怎样理解面向对象的

面向对象是利用编程语言对现实事物进行抽象。面向对象具有以下四大特征：

**（1）继承：**继承是从已有类得到继承信息创建新类的过程

**（2）封装：**通常认为封装是把数据和操作数据的方法绑定起来，对数据的访问只能通过已定义的接口。

**（3）多态性：**多态性是指允许不同子类型的对象对同一消息作出不同的响应。

**（4）抽象：**抽象是将一类对象的共同特征总结出来构造类的过程，包括数据抽象和行为抽象两方面。

<!-- more -->

## 3.2 int和Integer有什么区别，以及以下程序结果

（1）Integer是int的包装类，int则是java的一种基本数据类型

（2）Integer变量必须实例化后才能使用，而int变量不需要

（3）Integer实际是对象的引用，当new一个Integer时，实际上是生成一个指针指向此对象；而int则是直接存储数据值

（4）Integer的默认值是null，int的默认值是0

```java
    package com.cactus.interview.chapter03;

    /** 
     */
    public class Test01 {

        public static void main(String[] args) {
            Integer a = 127;
            Integer b = 127;
            Integer c = 128;
            Integer d = 128;
   /** 
     * @author : atguigu.com
     * @since 2019/7/28 
         Integer内部维护了一个IntegerCache缓冲区，范围是从-128到+127范围的 
         Integer类型数组。只要Integer赋值在-128到+127范围内，统一都是用次缓 
         冲区中的数据。如果不在此范围，则新创建对象。
     */
            System.out.println(a == b); //true  
            System.out.println(c == d); //false  
        }
    } 
```

## 3.3 ==和Equals区别

（1） ==

如果比较的是基本数据类型，那么比较的是变量的值

如果比较的是引用数据类型，那么比较的是地址值（两个对象是否指向同一块内存）

（2）equals

如果没重写equals方法比较的是两个对象的地址值

如果重写了equals方法后我们往往比较的是对象中的属性的内容

equals()方法最初在Object类中定义的，默认的实现就是使用==

![img](http://www.atguigu.com/wp-content/uploads/image011.png)

## 3.4 谈谈你对反射的理解

**（1）反射机制:**

所谓的反射机制就是java语言在运行时拥有一项自观的能力。通过这种能力可以彻底的了解自身的情况为下一步的动作做准备。

Java的反射机制的实现要借助于4个类：Class，Constructor，Field，Method;

其中Class代表的是类对 象，Constructor－类的构造器对象，Field－类的属性对象，Method－类的方法对象。通过这四个对象我们可以粗略的看到一个类的各个组 成部分。

**（2）Java反射的作用：**

在Java运行时环境中，对于任意一个类，可以知道这个类有哪些属性和方法。对于任意一个对象，可以调用它的任意一个方法。这种动态获取类的信息以及动态调用对象的方法的功能来自于Java 语言的反射（Reflection）机制。

**（3）Java 反射机制提供功能**

在运行时判断任意一个对象所属的类。

在运行时构造任意一个类的对象。

在运行时判断任意一个类所具有的成员变量和方法。

在运行时调用任意一个对象的方法

## 3.5 ArrarList和LinkedList区别

（1）ArrayList是实现了基于动态数组的数据结构，LinkedList基于链表的数据结构。

（2）对于随机访问get和set，ArrayList绝对优于LinkedList，因为LinkedList要移动指针。

（3）对于插入和删除操作add和remove，LinkedList比较占优势，因为ArrayList每插入或删除一条数据，都要移动插入点或删除点及之后的所有数据。

## 3.6 HashMap底层源码，数据结构

HashMap的底层结构在jdk1.7中由数组+链表实现，在jdk1.8中由数组+链表+红黑树实现，以数组+链表的结构为例。

![img](http://www.atguigu.com/wp-content/uploads/image014.jpg)

![img](http://www.atguigu.com/wp-content/uploads/image015.png)

**JDK1.8之前put方法：**

![img](http://www.atguigu.com/wp-content/uploads/image017.png)

**JDK1.8之后put方法：**

![img](http://www.atguigu.com/wp-content/uploads/4-28.png)

![img](http://www.atguigu.com/wp-content/uploads/6-17.png)

## 3.7 HashMap和Hashtable区别

**（1）线程安全性不同**

HashMap是线程不安全的，Hashtable是线程安全的，其中的方法是Synchronized的，在多线程并发的情况下，可以直接使用Hashtable，但是使用HashMap时必须自己增加同步处理。

**（2）是否提供contains方法**

HashMap只有containsValue和containsKey方法；Hashtable有contains、containsKey和containsValue三个方法，其中contains和containsValue方法功能相同。

**（3）key和value是否允许null值**

Hashtable中，key和value都不允许出现null值。HashMap中，null可以作为键，这样的键只有一个；可以有一个或多个键所对应的值为null。

**（4）数组初始化和扩容机制**

Hashtable在不指定容量的情况下的默认容量为11，而HashMap为16，Hashtable不要求底层数组的容量一定要为2的整数次幂，而HashMap则要求一定为2的整数次幂。

Hashtable扩容时，将容量变为原来的2倍加1，而HashMap扩容时，将容量变为原来的2倍。

## 3.8 TreeSet和HashSet区别

HashSet是采用hash表来实现的。其中的元素没有按顺序排列，add()、remove()以及contains()等方法都是复杂度为O(1)的方法。

TreeSet是采用树结构实现(红黑树算法)。元素是按顺序进行排列，但是add()、remove()以及contains()等方法都是复杂度为O(log (n))的方法。它还提供了一些方法来处理排序的set，如first(), last(), headSet(), tailSet()等等。

## 3.9 StringBuffer和StringBuilder区别

（1）StringBuffer 与 StringBuilder 中的方法和功能完全是等价的，

（2）只是StringBuffer 中的方法大都采用了 synchronized 关键字进行修饰，因此是线程安全的，而 StringBuilder 没有这个修饰，可以被认为是线程不安全的。 

（3）在单线程程序下，StringBuilder效率更快，因为它不需要加锁，不具备多线程安全而StringBuffer则每次都需要判断锁，效率相对更低

## 3.10 Final、Finally、Finalize

**final：**修饰符（关键字）有三种用法：修饰类、变量和方法。修饰类时，意味着它不能再派生出新的子类，即不能被继承，因此它和abstract（abstract修饰的类通常都需要子类来继承）在使用上可以理解为互斥的。修饰变量时，该变量使用中不被改变，必须在声明时给定初值，在引用中只能读取不可修改，即为常量。修饰方法时，也同样只能使用，不能在子类中被重写。

**finally：**通常放在try…catch的后面构造最终执行代码块，这就意味着程序无论正常执行还是发生异常，这里的代码只要JVM不关闭都能执行，可以将释放外部资源的代码写在finally块中。

**finalize：**Object类中定义的方法，Java中允许使用finalize() 方法在垃圾收集器将对象从内存中清除出去之前做必要的清理工作。这个方法是由垃圾收集器在销毁对象时调用的，通过重写finalize() 方法可以整理系统资源或者执行其他清理工作。

## 3.11 什么是 java 序列化，如何实现 java 序列化？

序列化就是一种用来处理对象流的机制，所谓对象流也就是将对象的内容进行流化。可以对流化后的对象进行读写操作，也可将流化后的对象传输于网络之间。序列化是为了解决在对对象流进行读写操作时所引发的问题。

序 列 化 的 实 现 ： 将 需 要 被 序 列 化 的 类 实 现 Serializable 接 口 ， 该 接 口 没 有 需 要 实 现 的 方 法 ， implements Serializable 只是为了标注该对象是可被序列化的，然后使用一个输出流(如：FileOutputStream)来构造一个ObjectOutputStream(对象流)对象，接着，使用 ObjectOutputStream 对象的 writeObject(Object obj)方法就可以将参数为 obj 的对象写出(即保存其状态)，要恢复的话则用输入流。

## 3.12 Object中有哪些方法

（1）protected Object clone()—>创建并返回此对象的一个副本。 
（2）boolean equals(Object obj)—>指示某个其他对象是否与此对象“相等”。 
（3）protected void finalize()—>当垃圾回收器确定不存在对该对象的更多引用时，由对象的垃圾回收器调用此方法。 
（4）Class<? extends Object> getClass()—>返回一个对象的运行时类。 
（5）int hashCode()—>返回该对象的哈希码值。 
（6）void notify()—>唤醒在此对象监视器上等待的单个线程。 
（7）void notifyAll()—>唤醒在此对象监视器上等待的所有线程。 
（8）String toString()—>返回该对象的字符串表示。 
（9）void wait()—>导致当前的线程等待，直到其他线程调用此对象的 notify() 方法或 notifyAll() 方法。 
    void wait(long timeout)—>导致当前的线程等待，直到其他线程调用此对象的 notify() 方法或 notifyAll()方法，或者超过指定的时间量。 
    void wait(long timeout, int nanos)—>导致当前的线程等待，直到其他线程调用此对象的 notify()

## 3.13 线程有几种状态，产生的条件是什么

![img](http://www.atguigu.com/wp-content/uploads/bc4e33a4150ac4ee79af80bf22f774e.png)

## 3.14 产生死锁的基本条件

**产生死锁的原因：**
（1） 因为系统资源不足。
（2） 进程运行推进的顺序不合适。
（3） 资源分配不当等。
    如果系统资源充足，进程的资源请求都能够得到满足，死锁出现的可能性就很低，否则
就会因争夺有限的资源而陷入死锁。其次，进程运行推进顺序与速度不同，也可能产生死锁。
**产生死锁的四个必要条件：

**（1） 互斥条件：一个资源每次只能被一个进程使用。
（2） 请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放。
（3） 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。
（4） 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。
    这四个条件是死锁的必要条件，只要系统发生死锁，这些条件必然成立，而只要上述条件之一不满足，就不会发生死锁。
**死锁的解除与预防：**
    理解了死锁的原因，尤其是产生死锁的四个必要条件，就可以最大可能地避免、预防和
解除死锁。所以，在系统设计、进程调度等方面注意如何不让这四个必要条件成立，如何确
定资源的合理分配算法，避免进程永久占据系统资源。此外，也要防止进程在处于等待状态
的情况下占用资源。因此，对资源的分配要给予合理的规划。

## 3.15 什么是线程池，如何使用？

线程池就是事先将多个线程对象放到一个容器中，当使用的时候就不用 new 线程而是直接去池中拿线程即可，节省了开辟子线程的时间，提高的代码执行效率。

在 JDK 的 java.util.concurrent.Executors 中提供了生成多种线程池的静态方法。

ExecutorService newCachedThreadPool = Executors.newCachedThreadPool();

ExecutorService newFixedThreadPool = Executors.newFixedThreadPool(4);

ScheduledExecutorService newScheduledThreadPool = Executors.newScheduledThreadPool(4);

ExecutorService newSingleThreadExecutor = Executors.newSingleThreadExecutor();

然后调用他们的 execute 方法即可。

**优点：**

第一：降低资源消耗。通过重复利用已创建的线程降低线程创建和销毁造成的消耗。

第二：提高响应速度。当任务到达时，任务可以不需要等到线程创建就能立即执行。

第三：提高线程的可管理性。线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。

## 3.16 Java自带有哪几种线程池？

## 一、ThreadPoolExecutor

ThreadPoolExecutor提供了四个构造方法：

![img](http://www.atguigu.com/wp-content/uploads/15900445121.png)

我们以最后一个构造方法（参数最多的那个），对其参数进行解释：

```java
    public ThreadPoolExecutor(int corePoolSize,                     // 1
        int maximumPoolSize,                    // 2
        long keepAliveTime,                  // 3
        TimeUnit unit,                         // 4
        BlockingQueue < Runnable > workQueue,     // 5
        ThreadFactory threadFactory,              // 6
        RejectedExecutionHandler handler) {     // 7
        if (corePoolSize < 0 || maximumPoolSize <= 0 ||
            maximumPoolSize < corePoolSize || keepAliveTime < 0)
            throw new IllegalArgumentException();
        if (workQueue == null || threadFactory == null || handler == null)
            throw new NullPointerException();
        this.corePoolSize = corePoolSize;
        this.maximumPoolSize = maximumPoolSize;
        this.workQueue = workQueue;
        this.keepAliveTime = unit.toNanos(keepAliveTime);
        this.threadFactory = threadFactory;
        this.handler = handler;
    }
```

![img](http://www.atguigu.com/wp-content/uploads/15900445431.png)

## 二、预定义线程池

JDK给我们预定义的几种线程池

### 1、FixedThreadPool

```java
  public static ExecutorService newFixedThreadPool(int nThreads) {
        return new ThreadPoolExecutor(nThreads, nThreads,
            0L, TimeUnit.MILLISECONDS,
            new LinkedBlockingQueue<Runnable>());
  }
```



- ePoolSize与maximumPoolSize相等，即其线程全为核心线程，是一个固定大小的线程池，是其优势；
- keepAliveTime = 0 该参数默认对核心线程无效，而FixedThreadPool全部为核心线程；
- workQueue 为LinkedBlockingQueue（无界阻塞队列），队列最大值为Integer.MAX_VALUE。如果任务提交速度持续大余任务处理速度，会造成队列大量阻塞。因为队列很大，很有可能在拒绝策略前，内存溢出。是其劣势；
- FixedThreadPool的任务执行是无序的；

适用场景：可用于Web服务瞬时削峰，但需注意长时间持续高峰情况造成的队列阻塞。

### 2、CachedThreadPool

```java
    public static ExecutorService newCachedThreadPool() {
        return new ThreadPoolExecutor(0, Integer.MAX_VALUE,
                                  60L, TimeUnit.SECONDS,
                                  new SynchronousQueue<Runnable>());
    }
```

- corePoolSize = 0，maximumPoolSize = Integer.MAX_VALUE，即线程数量几乎无限制；
- keepAliveTime = 60s，线程空闲60s后自动结束。
- workQueue 为 SynchronousQueue 同步队列，这个队列类似于一个接力棒，入队出队必须同时传递，因为CachedThreadPool线程创建无限制，不会有队列等待，所以使用SynchronousQueue；

适用场景：快速处理大量耗时较短的任务，如Netty的NIO接受请求时，可使用CachedThreadPool。

### 3、SingleThreadExecutor

```java
  public static ExecutorService newSingleThreadExecutor() {
        return new FinalizableDelegatedExecutorService(
            new ThreadPoolExecutor(1, 1, 0L, TimeUnit.MILLISECONDS,
                new LinkedBlockingQueue<Runnable>()));
    }
```

这里多了一层FinalizableDelegatedExecutorService包装，以下代码解释一下其作用：

```java
 public static void main(String[] args) {
        ExecutorService fixedExecutorService = Executors.newFixedThreadPool(1);
        ThreadPoolExecutor threadPoolExecutor = (ThreadPoolExecutor) fixedExecutorService;
        System.out.println(threadPoolExecutor.getMaximumPoolSize());
        threadPoolExecutor.setCorePoolSize(8);
        
        ExecutorService singleExecutorService = Executors.newSingleThreadExecutor();
// 运行时异常 java.lang.ClassCastException
//ThreadPoolExecutor threadPoolExecutor2 = (ThreadPoolExecutor) singleExecutorService;
    }
```

对比可以看出，FixedThreadPool可以向下转型为ThreadPoolExecutor，并对其线程池进行配置，而SingleThreadExecutor被包装后，无法成功向下转型。因此，SingleThreadExecutor被定以后，无法修改，做到了真正的Single。

### 4、ScheduledThreadPool

```java
   public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize) {
        return new ScheduledThreadPoolExecutor(corePoolSize);
    }

    newScheduledThreadPool调用的是ScheduledThreadPoolExecutor的构造方法，而ScheduledThreadPoolExecutor继承了ThreadPoolExecutor，构造是还是调用了其父类的构造方法。
    public ScheduledThreadPoolExecutor(int corePoolSize) {
        super(corePoolSize, Integer.MAX_VALUE, 0, NANOSECONDS,
            new DelayedWorkQueue());
    }
```



## 三、自定义线程池

以下是自定义线程池，使用了有界队列，自定义ThreadFactory和拒绝策略的demo：

```java
public class ThreadTest {

    public static void main(String[] args) throws InterruptedException, IOException {
        int corePoolSize = 2;
        int maximumPoolSize = 4;
        long keepAliveTime = 10;
        TimeUnit unit = TimeUnit.SECONDS;
        BlockingQueue<Runnable> workQueue = new ArrayBlockingQueue<>(2);
        ThreadFactory threadFactory = new NameTreadFactory();
        RejectedExecutionHandler handler = new MyIgnorePolicy();
        ThreadPoolExecutor executor 
= new ThreadPoolExecutor(corePoolSize, maximumPoolSize, keepAliveTime, unit,
                                  workQueue, threadFactory, handler);
        executor.prestartAllCoreThreads(); // 预启动所有核心线程
        
        for (int i = 1; i <= 10; i++) {
            MyTask task = new MyTask(String.valueOf(i));
            executor.execute(task);
        }

        System.in.read(); //阻塞主线程
    }

    static class NameTreadFactory implements ThreadFactory {

        private final AtomicInteger mThreadNum = new AtomicInteger(1);

        @Override
        public Thread newThread(Runnable r) {
            Thread t = new Thread(r, "my-thread-" + mThreadNum.getAndIncrement());
            System.out.println(t.getName() + " has been created");
            return t;
        }
    }

    public static class MyIgnorePolicy implements RejectedExecutionHandler {

        public void rejectedExecution(Runnable r, ThreadPoolExecutor e) {
            doLog(r, e);
        }

        private void doLog(Runnable r, ThreadPoolExecutor e) {
            // 可做日志记录等
            System.err.println( r.toString() + " rejected");
// System.out.println("completedTaskCount: " + e.getCompletedTaskCount());
        }
    }

    static class MyTask implements Runnable {
        private String name;

        public MyTask(String name) {
            this.name = name;
        }

        @Override
        public void run() {
            try {
                System.out.println(this.toString() + " is running!");
                Thread.sleep(3000); //让任务执行慢点
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }

        public String getName() {
            return name;
        }

        @Override
        public String toString() {
            return "MyTask [name=" + name + "]";
        }
}
}
```



## 3.17 Java 中有几种类型的流

![img](http://www.atguigu.com/wp-content/uploads/1-66.png)

![img](http://www.atguigu.com/wp-content/uploads/2-50.png)

![img](http://www.atguigu.com/wp-content/uploads/3-35.png)

![img](http://www.atguigu.com/wp-content/uploads/4-27.png)

## 3.18 字节流如何转为字符流

字节输入流转字符输入流通过 InputStreamReader 实现，该类的构造函数可以传入 InputStream 对象。

字符输出流转字节输出流通过OutputStreamWriter 实现，该类的构造函数可以传入 OutputStream 对象。

## 3.19 请写出你最常见的5个Exception

（1）java.lang.NullPointerException 空指针异常；出现原因：调用了未经初始化的对象或者是不存在的对象。

（2）java.lang.ClassNotFoundException 指定的类找不到；出现原因：类的名称和路径加载错误；通常都是程序试图通过字符串来加载某个类时可能引发异常。

（3）java.lang.NumberFormatException 字符串转换为数字异常；出现原因：字符型数据中包含非数字型字符。

（4）java.lang.IndexOutOfBoundsException 数组角标越界异常，常见于操作数组对象时发生。

（5）java.lang.IllegalArgumentException 方法传递参数错误。

（6）java.lang.ClassCastException 数据类型转换异常。

## 4. JVM

## 4.1 JVM内存分哪几个区，每个区的作用是什么?

![img](http://www.atguigu.com/wp-content/uploads/image026.png)

java虚拟机主要分为以下几个区:

**（1）方法区**：

1. a. JDK7中称为永久代，JDK8及之后称为元空间，在该区内很少发生垃圾回收，但是并不代表不发生GC，在这里进行的GC主要是对方法区里的常量池和对类型的卸载
2. b. 方法区主要用来存储已被虚拟机加载的类的信息、常量、静态变量和即时编译器编译后的代码等数据。
3. c. 该区域是被线程共享的。
4. d. 方法区里有一个运行时常量池，用于存放静态编译产生的字面量和符号引用。该常量池具有动态性，也就是说常量并不一定是编译时确定，运行时生成的常量也会存在这个常量池中。

**（2）虚拟机栈**:

1. a. 虚拟机栈也就是我们平常所称的栈内存,它为java方法服务，每个方法在执行的时候都会创建一个栈帧，用于存储局部变量表、操作数栈、动态链接和方法出口等信息。
2. b. 虚拟机栈是线程私有的，它的生命周期与线程相同。
3. c. 局部变量表里存储的是基本数据类型、returnAddress类型（指向一条字节码指令的地址）和对象引用，这个对象引用有可能是指向对象起始地址的一个指针，也有可能是代表对象的句柄或者与对象相关联的位置。局部变量所需的内存空间在编译器间确定
4. d. 操作数栈的作用主要用来存储运算结果以及运算的操作数，它不同于局部变量表通过索引来访问，而是压栈和出栈的方式
5. e. 每个栈帧都包含一个指向运行时常量池中该栈帧所属方法的引用，持有这个引用是为了支持方法调用过程中的动态连接.动态链接就是将常量池中的符号引用在运行期转化为直接引用。

**（3）本地方法栈**：
本地方法栈和虚拟机栈类似，只不过本地方法栈为Native方法服务。

**（4）堆**：

java堆是所有线程所共享的一块内存，在虚拟机启动时创建，几乎所有的对象实例都在这里创建，因此该区域经常发生垃圾回收操作。

**（5）程序计数器：**

内存空间小，字节码解释器工作时通过改变这个计数值可以选取下一条需要执行的字节码指令，分支、循环、跳转、异常处理和线程恢复等功能都需要依赖这个计数器完成。该内存区域是唯一一个java虚拟机规范没有规定任何OOM情况的区域。

## 4.2 heap 和stack 有什么区别

**（1）申请方式**

stack:由系统自动分配。例如，声明在函数中一个局部变量 int b; 系统自动在栈中为 b 开辟空间

heap:需要程序员自己申请，并指明大小，在 c 中 malloc 函数，对于Java 需要手动 new Object()的形式开辟

**（2）申请后系统的响应**

stack：只要栈的剩余空间大于所申请空间，系统将为程序提供内存，否则将报异常提示栈溢出。

heap：首先应该知道操作系统有一个记录空闲内存地址的链表，当系统收到程序的申请时，会遍历该链表，寻找第一个空间大于所申请空间的堆结点，然后将该结点从空闲结点链表中删除，并将该结点的空间分配给程序。另外，由于找到的堆结点的大小不一定正好等于申请的大小，系统会自动的将多余的那部分重新放入空闲链表中。

**（3）申请大小的限制**

stack：栈是向低地址扩展的数据结构，是一块连续的内存的区域。这句话的意思是栈顶的地址和栈的最大容量是系统预先规定好的，在 WINDOWS 下，栈的大小是 2M（默认值也取决于虚拟内存的大小），如果申请的空间超过栈的剩余空间时，将提示 overflow。因此，能从栈获得的空间较小。

heap：堆是向高地址扩展的数据结构，是不连续的内存区域。这是由于系统是用链表来存储的空闲内存地址的， 自然是不连续的，而链表的遍历方向是由低地址向高地址。堆的大小受限于计算机系统中有效的虚拟内存。由此可见， 堆获得的空间比较灵活，也比较大。

**（4）申请效率的比较**

stack：由系统自动分配，速度较快。但程序员是无法控制的。

heap：由 new 分配的内存，一般速度比较慢，而且容易产生内存碎片,不过用起来最方便。

**（5）heap和stack中的存储内容**

stack：在函数调用时，第一个进栈的是主函数中后的下一条指令（函数调用语句的下一条可执行语句）的地址， 然后是函数的各个参数，在大多数的 C 编译器中，参数是由右往左入栈的，然后是函数中的局部变量。注意静态变量是不入栈的。

当本次函数调用结束后，局部变量先出栈，然后是参数，最后栈顶指针指向最开始存的地址，也就是主函数中的下一条指令，程序由该点继续运行。

heap：一般是在堆的头部用一个字节存放堆的大小。堆中的具体内容有程序员安排。

## 4.3 java类加载过程?

Java类加载需要经历一下几个过程：

**（1）加载**

加载时类加载的第一个过程，在这个阶段，将完成一下三件事情：

1. a. 通过一个类的全限定名获取该类的二进制流。
2. b. 将该二进制流中的静态存储结构转化为方法去运行时数据结构。 
3. c. 在内存中生成该类的Class对象，作为该类的数据访问入口。

**（2）链接**

**2.1）验证**

验证的目的是为了确保Class文件的字节流中的信息不会危害到虚拟机.在该阶段主要完成以下四钟验证:

1. a. 文件格式验证：验证字节流是否符合Class文件的规范，如主次版本号是否在当前虚拟机范围内，常量池中的常量是否有不被支持的类型.
2. b. 元数据验证:对字节码描述的信息进行语义分析，如这个类是否有父类，是否继承了不被继承的类等。
3. c. 字节码验证：是整个验证过程中最复杂的一个阶段，通过验证数据流和控制流的分析，确定程序语义是否正确，主要针对方法体的验证。如：方法中的类型转换是否正确，跳转指令是否正确等。
4. d. 符号引用验证：这个动作在后面的解析过程中发生，主要是为了确保解析动作能正确执行。
5. **2.2）准备**

准备阶段是为类的静态变量分配内存并将其初始化为默认值，这些内存都将在方法区中进行分配。准备阶段不分配类中的实例变量的内存，实例变量将会在对象实例化时随着对象一起分配在Java堆中。

**2.3）解析**

该阶段主要完成符号引用到直接引用的转换动作。解析动作并不一定在初始化动作完成之前，也有可能在初始化之后。

**（3）初始化** 初始化时类加载的最后一步，前面的类加载过程，除了在加载阶段用户应用程序可以通过自定义类加载器参与之外，其余动作完全由虚拟机主导和控制。到了初始化阶段，才真正开始执行类中定义的Java程序代码。

## 4.4 什么是类加载器，类加载器有哪些?

实现通过类的全限定名获取该类的二进制字节流的代码块叫做类加载器。

主要有以下四种类加载器:

（1）启动类加载器(Bootstrap ClassLoader)用来加载java核心类库，无法被java程序直接引用。

（2）扩展类加载器(extensions class loader):它用来加载 Java 的扩展库。Java 虚拟机的实现会提供一个扩展库目录。该类加载器在此目录里面查找并加载 Java 类。

（3）系统类加载器（system class loader）也叫应用类加载器：它根据 Java 应用的类路径（CLASSPATH）来加载 Java 类。一般来说，Java 应用的类都是由它来完成加载的。可以通过 ClassLoader.getSystemClassLoader()来获取它。

（4）用户自定义类加载器，通过继承 java.lang.ClassLoader类的方式实现。

## 4.5 java中垃圾收集的方法有哪些?

**1）引用计数法算法**  应用于：微软的COM/ActionScrip3/Python等

a) 如果对象没有被引用，就会被回收，缺点：需要维护一个引用计算器

**2）可达性分析算法** 以根对象集合(GC Roots)为起始点，按照从上至下的方式搜索被根对象集合所连接的目标对象是否可达。不可达的，就意味着该对象己经死亡，可以标记为垃圾对象。

**3)复制算法** 年轻代中使用的是Minor GC，这种GC算法采用的是复制算法(Copying)

a) 效率高，缺点：需要内存容量大，比较耗内存

b) 使用在占空间比较小、刷新次数多的新生区

**4）标记-清除算法** 老年代一般是由标记清除或者是标记清除与标记整理的混合实现

a) 效率比较低，会产生碎片。

**5）标记-压缩算法** 老年代一般是由标记清除或者是标记清除与标记整理的混合实现

a) 效率低速度慢，需要移动对象，但不会产生碎片。

**6）标记-清除-压缩算法** 标记清除-标记压缩的集合，多次GC后才Compact

a) 使用于占空间大刷新次数少的养老区，是4)和5)的集合体

## 4.6 如何判断一个对象是否存活?(或者GC对象的判定方法)

判断一个对象是否存活有两种方法:

**（1）引用计数法**

所谓引用计数法就是给每一个对象设置一个引用计数器，每当有一个地方引用这个对象时，就将计数器加一，引用失效时，计数器就减一。当一个对象的引用计数器为零时，说明此对象没有被引用，也就是“死对象”,将会被垃圾回收.

引用计数法有一个缺陷就是无法解决循环引用问题，也就是说当对象A引用对象B，对象B又引用者对象A，那么此时A,B对象的引用计数器都不为零，也就造成无法完成垃圾回收，所以主流的虚拟机都没有采用这种算法。

**（2）可达性算法(引用链法)**

该算法的基本思路就是通过以GC Roots对象作为起点，从这些节点开始向下搜索，搜索走过的路径被称为引用链（Reference Chain)，当一个对象到GC Roots没有任何引用链相连时（即从GC Roots节点到该节点不可达），则证明该对象是不可用的。

在java中可以作为GC Roots的对象有以下几种：虚拟机栈中引用的对象、方法区类静态属性引用的对象、方法区常量池引用的对象、本地方法栈JNI引用的对象。

## 4.7 简述java内存分配与回收策略以及Minor GC和Major GC（full GC）

**内存分配：**

**（1）栈区**：栈分为java虚拟机栈和本地方法栈

**（2）堆区**：堆被所有线程共享区域，在虚拟机启动时创建，唯一目的存放对象实例。堆区是gc的主要区域，通常情况下分为两个区块年轻代和年老代。更细一点年轻代又分为Eden区，主要放新创建对象，From survivor 和 To survivor 保存gc后幸存下的对象，默认情况下各自占比 8:1:1。

**（3）方法区**：被所有线程共享区域，用于存放已被虚拟机加载的类信息，常量，静态变量等数据。被Java虚拟机描述为堆的一个逻辑部分。习惯上也叫它永久代（permanment generation）

**（4）程序计数器**：当前线程所执行的行号指示器。通过改变计数器的值来确定下一条指令，比如循环，分支，跳转，异常处理，线程恢复等都是依赖计数器来完成。线程私有的。

**回收策略以及Minor GC和Major GC：**

（1）对象优先在堆的Eden区分配。

（2）大对象直接进入老年代。

（3）长期存活的对象将直接进入老年代。

当Eden区没有足够的空间进行分配时，虚拟机会执行一次Minor GC.Minor GC通常发生在新生代的Eden区，在这个区的对象生存期短，往往发生GC的频率较高，回收速度比较快;Full Gc/Major GC 发生在老年代，一般情况下，触发老年代GC的时候不会触发Minor GC,但是通过配置，可以在Full GC之前进行一次Minor GC这样可以加快老年代的回收速度。

## 5. 设计模式

## 5.1 你所知道的设计模式有哪些

Java 中一般认为有 23 种设计模式，我们不需要所有的都会，但是其中常用的几种设计模式应该去掌握。下面列出了所有的设计模式。需要掌握的设计模式我单独列出来了，当然能掌握的越多越好。

总体来说设计模式分为三大类：

创建型模式，共5种：工厂方法模式、抽象工厂模式、单例模式、建造者模式、原型模式。

结构型模式，共7种：适配器模式、装饰器模式、代理模式、外观模式、桥接模式、组合模式、享元模式。

行为型模式，共11种：策略模式、模板方法模式、观察者模式、迭代子模式、责任链模式、命令模式、备忘录模式、状态模式、访问者模式、中介者模式、解释器模式。

## 5.2 单例设计模式

见【第2章 手写代码 2.5】

## 5.3 工厂设计模式（Factory）

### 5.3.1 什么是工厂设计模式？

工厂设计模式，顾名思义，就是用来生产对象的，在java中，万物皆对象，这些对象都需要创建，如果创建的时候直接new该对象，就会对该对象耦合严重，假如我们要更换对象，所有new对象的地方都需要修改一遍，这显然违背了软件设计的开闭原则，如果我们使用工厂来生产对象，我们就只和工厂打交道就可以了，彻底和对象解耦，如果要更换对象，直接在工厂里更换该对象即可，达到了与对象解耦的目的；所以说，工厂模式最大的优点就是：解耦

### 5.3.2 简单工厂（Simple Factory）

**定义：**

一个工厂方法，依据传入的参数，生成对应的产品对象；
**角色：**
1、抽象产品
2、具体产品
3、具体工厂
4、产品使用者
**使用说明：**

先将产品类抽象出来，比如，苹果和梨都属于水果，抽象出来一个水果类Fruit，苹果和梨就是具体的产品类，然后创建一个水果工厂，分别用来创建苹果和梨。代码如下：

**水果接口：**

```java
public interface Fruit {  
  void whatIm();  
} 
```

**苹果类：**

```java
public class Apple implements Fruit {  
    @Override  
    public void whatIm() {  
        System.out.println("苹果");  
    }  
}  
```

**梨类：**

```java
public class Pear implements Fruit {  
    @Override  
    public void whatIm() {  
        System.out.println("梨");  
    }  
}  
```

**水果工厂：**

```java
public class FruitFactory {  
  
    public Fruit createFruit(String type) {  
  
        if (type.equals("apple")) {//生产苹果  
            return new Apple();  
        } else if (type.equals("pear")) {//生产梨  
            return new Pear();  
        }  
  
        return null;  
    }  
}  
```

**使用工厂生产产品：**

```java
public class FruitApp {  
  
    public static void main(String[] args) {  
        FruitFactory mFactory = new FruitFactory();  
        Apple apple = (Apple) mFactory.createFruit("apple");//获得苹果  
        Pear pear = (Pear) mFactory.createFruit("pear");//获得梨  
        apple.whatIm();  
        pear.whatIm();  
    }  
}  
```

以上的这种方式，每当添加一种水果，就必然要修改工厂类，违反了开闭原则；

所以简单工厂只适合于产品对象较少，且产品固定的需求，对于产品变化无常的需求来说显然不合适。

### 5.3.3 工厂方法（Factory Method）

**定义：**

将工厂提取成一个接口或抽象类，具体生产什么产品由子类决定；
**角色：**
1、抽象产品
2、具体产品
3、抽象工厂
4、具体工厂
**使用说明：**

和上例中一样，产品类抽象出来，这次我们把工厂类也抽象出来，生产什么样的产品由子类来决定。代码如下：
**水果接口、苹果类和梨类：**

代码和上例一样

**抽象工厂接口：**

```java
public interface FruitFactory {  
    Fruit createFruit();//生产水果  
}  
```

**苹果工厂：**

```java
public class AppleFactory implements FruitFactory {  
    @Override  
    public Apple createFruit() {  
        return new Apple();  
    }  
}  
```

**梨工厂：**

```java
public class PearFactory implements FruitFactory {  
    @Override  
    public Pear createFruit() {  
        return new Pear();  
    }  
}  
```

**使用工厂生产产品：**

```java
public class FruitApp {  
  
    public static void main(String[] args){  
        AppleFactory appleFactory = new AppleFactory();  
        PearFactory pearFactory = new PearFactory();  
        Apple apple = appleFactory.createFruit();//获得苹果  
        Pear pear = pearFactory.createFruit();//获得梨  
        apple.whatIm();  
        pear.whatIm();  
    }  
}  
```

以上这种方式，虽然解耦了，也遵循了开闭原则，但是如果我需要的产品很多的话，需要创建非常多的工厂，所以这种方式的缺点也很明显。

### 5.3.4 抽象工厂（Abstract Factory）

**定义：**

为创建一组相关或者是相互依赖的对象提供的一个接口，而不需要指定它们的具体类。
**角色：**

1. 1、抽象产品
   2、具体产品
   3、抽象工厂
   4、具体工厂

**使用说明：**

抽象工厂和工厂方法的模式基本一样，区别在于，工厂方法是生产一个具体的产品，而抽象工厂可以用来生产一组相同，有相对关系的产品；重点在于一组，一批，一系列；举个例子，假如生产小米手机，小米手机有很多系列，小米note、红米note等；假如小米note生产需要的配件有825的处理器，6英寸屏幕，而红米只需要650的处理器和5寸的屏幕就可以了。用抽象工厂来实现：

**cpu接口和实现类：**

```java
public interface Cpu {  
    void run();  
    class Cpu650 implements Cpu {  
        @Override  
        public void run() {  
            System.out.println("650 也厉害");  
        }  
    }  
    class Cpu825 implements Cpu {  
        @Override  
        public void run() {  
            System.out.println("825 更强劲");  
        }  
    }  
}  
```

**屏幕接口和实现类：**

```java
public interface Screen {  
    void size();  
    class Screen5 implements Screen {  
  
        @Override  
        public void size() {  
            System.out.println("" +  
                    "5寸");  
        }  
    }  
    class Screen6 implements Screen {  
  
        @Override  
        public void size() {  
            System.out.println("6寸");  
        }  
    }  
}  
```

**抽象工厂接口：**

```java
public interface PhoneFactory {  
    Cpu getCpu();//使用的cpu  
    Screen getScreen();//使用的屏幕  
}  
```

**小米手机工厂：**

```java
public class XiaoMiFactory implements PhoneFactory {  
    @Override  
    public Cpu.Cpu825 getCpu() {  
        return new Cpu.Cpu825();//高性能处理器  
    }  
    @Override  
    public Screen.Screen6 getScreen() {  
        return new Screen.Screen6();//6寸大屏  
    }  
}  
```

**红米手机工厂：**

```java
public class HongMiFactory implements PhoneFactory {  
  
    @Override  
    public Cpu.Cpu650 getCpu() {  
        return new Cpu.Cpu650();//高效处理器  
    }  
    @Override  
    public Screen.Screen5 getScreen() {  
        return new Screen.Screen5();//小屏手机  
    }  
}  
```

**使用工厂生产产品：**

```java
public class PhoneApp {  
    public static void main(String[] args){  
        HongMiFactory hongMiFactory = new HongMiFactory();  
        XiaoMiFactory xiaoMiFactory = new XiaoMiFactory();  
        Cpu.Cpu650 cpu650 = hongMiFactory.getCpu();  
        Cpu.Cpu825 cpu825 = xiaoMiFactory.getCpu();  
        cpu650.run();  
        cpu825.run();  
        Screen.Screen5 screen5 = hongMiFactory.getScreen();  
        Screen.Screen6 screen6 = xiaoMiFactory.getScreen();  
        screen5.size();  
        screen6.size();  
    }  
}  
```

以上例子可以看出，抽象工厂可以解决一系列的产品生产的需求，对于大批量，多系列的产品，用抽象工厂可以更好的管理和扩展。

### 5.3.5三种工厂方式总结

1、对于简单工厂和工厂方法来说，两者的使用方式实际上是一样的，如果对于产品的分类和名称是确定的，数量是相对固定的，推荐使用简单工厂模式；

2、抽象工厂用来解决相对复杂的问题，适用于一系列、大批量的对象生产。

## 5.4 代理模式（Proxy）

### 5.4.1什么是代理模式？

代理模式给某一个对象提供一个代理对象，并由代理对象控制对原对象的引用。通俗的来讲代理模式就是我们生活中常见的中介。

举个例子来说明：假如说我现在想买一辆二手车，虽然我可以自己去找车源，做质量检测等一系列的车辆过户流程，但是这确实太浪费我得时间和精力了。我只是想买一辆车而已为什么我还要额外做这么多事呢？于是我就通过中介公司来买车，他们来给我找车源，帮我办理车辆过户流程，我只是负责选择自己喜欢的车，然后付钱就可以了。用图表示如下：

![IMG_256](http://www.atguigu.com/wp-content/uploads/image028.png)

### 5.4.2 为什么要用代理模式？

**中介隔离作用：**

在某些情况下，一个客户类不想或者不能直接引用一个委托对象，而代理类对象可以在客户类和委托对象之间起到中介的作用，其特征是代理类和委托类实现相同的接口。

**开闭原则，增加功能：**

代理类除了是客户类和委托类的中介之外，我们还可以通过给代理类增加额外的功能来扩展委托类的功能，这样做我们只需要修改代理类而不需要再修改委托类，符合代码设计的开闭原则。代理类主要负责为委托类预处理消息、过滤消息、把消息转发给委托类，以及事后对返回结果的处理等。代理类本身并不真正实现服务，而是同过调用委托类的相关方法，来提供特定的服务。真正的业务功能还是由委托类来实现，但是可以在业务功能执行的前后加入一些公共的服务。例如我们想给项目加入缓存、日志这些功能，我们就可以使用代理类来完成，而没必要修改已经封装好的委托类。

### 5.4.3 有哪几种代理模式？

我们有多种不同的方式来实现代理。

如果按照代理创建的时期来进行分类的话，可以分为两种：静态代理、动态代理。

- ● 静态代理是由程序员创建或特定工具自动生成源代码，再对其编译。在程序员运行之前，代理类.class文件就已经被创建了。
- ● 动态代理是在程序运行时通过反射机制动态创建的。

### 5.4.4 静态代理（Static Proxy）

**第一步：创建服务类接口**

```java
public interface BuyHouse {  
    void buyHouse();  
}  
```

**第二步：实现服务接口**

```java
public class BuyHouseImpl implements BuyHouse {  
    @Override  
    public void buyHouse() {  
        System.out.println("我要买房");  
    }  
}  
```

**第三步：创建代理类**

```java
 public class BuyHouseProxy implements BuyHouse {  
  
    private BuyHouse buyHouse;  
  
    public BuyHouseProxy(final BuyHouse buyHouse) {  
        this.buyHouse = buyHouse;  
    }  
    @Override  
    public void buyHouse() {  
        System.out.println("买房前准备");  
        buyHouse.buyHouse();  
        System.out.println("买房后装修");  
  
    }  
}  
```

**第四步：编写测试类**

```java
public class HouseApp {  
  
    public static void main(String[] args) {  
        BuyHouse buyHouse = new BuyHouseImpl();  
        BuyHouseProxy buyHouseProxy = new BuyHouseProxy(buyHouse);  
        buyHouseProxy.buyHouse();  
    }  
}  
```

 Proxy是所有动态生成的代理的共同的父类，这个类有一个静态方法Proxy.newProxyInstance()，接收三个参数：

- ● ClassLoader loader：指定当前目标对象使用的类加载器,获取加载器的方法是固定的
- ● Class<?>[] interfaces：指定目标对象实现的接口的类型,使用泛型方式确认类型
- ● InvocationHandler：指定动态处理器，执行目标对象的方法时,会触发事件处理器的方法

**JDK动态代理总结：**

优点：相对于静态代理，动态代理大大减少了开发任务，同时减少了对业务接口的依赖，降低了耦合度。

缺点：Proxy是所有动态生成的代理的共同的父类，因此服务类必须是接口的形式，不能是普通类的形式，因为Java无法实现多继承。

### 5.4.6 CGLib动态代理（CGLib Proxy）

JDK实现动态代理需要实现类通过接口定义业务方法，对于没有接口的类，如何实现动态代理呢，这就需要CGLib了。CGLib采用了底层的字节码技术，其原理是通过字节码技术为一个类创建子类，并在子类中采用方法拦截的技术拦截所有父类方法的调用，顺势织入横切逻辑。但因为采用的是继承，所以不能对final修饰的类进行代理。JDK动态代理与CGLib动态代理均是实现Spring AOP的基础。

**Cglib子类代理实现方法：**

（1）引入cglib的jar文件，asm的jar文件

（2）代理的类不能为final

（3）目标业务对象的方法如果为final/static，那么就不会被拦截，即不会执行目标对象额外的业务方法

**第一步：创建服务类**

```java
public class BuyHouse2 {  
  
    public void buyHouse() {  
        System.out.println("我要买房");  
    }  
} 
```

**第二步：创建CGLIB代理类**

```java
public class CglibProxy implements MethodInterceptor {  
  
    private Object target;  
  
    public CglibProxy(Object target) {  
        this.target = target;  
    }  
  
    /** 
     *  给目标对象创建一个代理对象 
     * @return 代理对象 
     */  
    public Object getProxyInstance() {  
        //1.工具类  
        Enhancer enhancer = new Enhancer();  
        //2.设置父类  
        enhancer.setSuperclass(target.getClass());  
        //3.设置回调函数  
        enhancer.setCallback(this);  
        //4.创建子类(代理对象)  
        return enhancer.create();  
  
    }  
  
    public Object intercept(Object object, Method method, Object[] args, MethodProxy methodProxy) throws Throwable {  
        System.out.println("买房前准备");  
        //执行目标对象的方法  
        Object result = method.invoke(target, args);  
        System.out.println("买房后装修");  
        return result;  
    }  
}  
```

**第三步：创建测试类**

```java
public class HouseApp {  
  
    public static void main(String[] args) {  
  
        BuyHouse2 target = new BuyHouse2();  
        CglibProxy cglibProxy = new CglibProxy(target);  
        BuyHouse2 buyHouseCglibProxy = (BuyHouse2) cglibProxy.getProxyInstance();  
        buyHouseCglibProxy.buyHouse();  
    }  
}  
```

**CGLib代理总结：** 

CGLib创建的动态代理对象比JDK创建的动态代理对象的性能更高，但是CGLIB创建代理对象时所花费的时间却比JDK多得多。所以对于单例的对象，因为无需频繁创建对象，用CGLIB合适，反之使用JDK方式要更为合适一些。同时由于CGLib由于是采用动态创建子类的方法，对于final修饰的方法无法进行代理。

### 5.4.7 简述动态代理的原理， 常用的动态代理的实现方式

动态代理的原理: **使用一个代理将对象包装起来**，然后用该代理对象取代原始对象。任何对原始对象的调用都要通过代理。

代理对象决定是否以及何时将方法调  用转到原始对象上

动态代理的方式

基于接口实现动态代理： JDK动态代理

基于继承实现动态代理： Cglib、Javassist动态代理

## 6. MySql

## 6.1 jdbc 操作数据库流程

第一步：Class.forName()加载数据库连接驱动；

第二步：DriverManager.getConnection()获取数据连接对象;

第三步：根据SQL 获取 sql 会话对象，有 2 种方式 Statement、PreparedStatement ;

第四步：执行SQL 处理结果集，执行 SQL 前如果有参数值就设置参数值 setXXX();

第五步：关闭结果集、关闭会话、关闭连接。

## 6.2 关系数据库中连接池的机制是什么？

前提：为数据库连接建立一个缓冲池。

（1）从连接池获取或创建可用连接

（2）使用完毕之后，把连接返回给连接池

（3）在系统关闭前，断开所有连接并释放连接占用的系统资源

（4）能够处理无效连接，限制连接池中的连接总数不低于或者不超过某个限定值。

其中有几个概念需要大家理解：

最小连接数是连接池一直保持的数据连接。如果应用程序对数据库连接的使用量不大，将会有大量的数据库连接资源被浪费掉。

最大连接数是连接池能申请的最大连接数。如果数据连接请求超过此数，后面的数据连接请求将被加入到等待队列中，这会影响之后的数据库操作。

如果最小连接数与最大连接数相差太大，那么，最先的连接请求将会获利，之后超过最小连接数量的连接请求等价于建立一个新的数据库连接。不过，这些大于最小连接数的数据库连接在使用完不会马上被释放，它将被放到连接池中等待重复使用或是空闲超时后被释放。

上面的解释，可以这样理解：数据库池连接数量一直保持一个不少于最小连接数的数量，当数量不够时，数据库会创建一些连接，直到一个最大连接数，之后连接数据库就会等待。

## 6.3 SQL 的select 语句完整的执行顺序

SQL Select 语句完整的执行顺序：

（1）from 子句组装来自不同数据源的数据；

（2）where 子句基于指定的条件对记录行进行筛选；

（3）group by 子句将数据划分为多个分组；

（4）使用聚集函数进行计算；

（5）使用 having 子句筛选分组；

（6）计算所有的表达式；

（7）select 的字段；

（8）使用order by 对结果集进行排序。

## 6.4 MySQL的事务

**事务的基本要素（ACID）：**

● 原子性（Atomicity） 原子性是指事务是一个不可分割的工作单位，事务中的操作要么都发生，要么都不发生。
● 一致性（Consistency） 事务必须使数据库从一个一致性状态变换到另外一个一致性状态。
● 隔离性（Isolation） 事务的隔离性是指一个事务的执行不能被其他事务干扰，即一个事务内部的操作及使用的数据对并发的其他事务是隔离的，并发执行的各个事务之间不能互相干扰。
● 持久性（Durability） 持久性是指一个事务一旦被提交，它对数据库中数据的改变就是永久性的，接下来的其他操作和数据库故障不应该对其有任何影响。

- 

**事务的并发问题：**

- ● 脏读：事务A读取了事务B更新的数据，然后B回滚操作，那么A读取到的数据是脏数据
- ● 不可重复读：事务 A 多次读取同一数据，事务 B 在事务A多次读取的过程中，对数据作了更新并提交，导致事务A多次读取同一数据时，结果 不一致
- ● 幻读：系统管理员A将数据库中所有学生的成绩从具体分数改为ABCDE等级，但是系统管理员B就在这个时候插入了一条具体分数的记录，当系统管理员A改结束后发现还有一条记录没有改过来，就好像发生了幻觉一样，这就叫幻读。

**小结：**

不可重复读的和幻读很容易混淆，不可重复读侧重于修改，幻读侧重于新增或删除。解决不可重复读的问题只需锁住满足条件的行，解决幻读需要锁表

**MySQL事务隔离级别：**

事务隔离级别                     					脏读       不可重复读      幻读

读未提交（read-uncommitted）       是         	是             		是

不可重复读（read-committed）        否         	是             		是

可重复读（repeatable-read）            否         	否             		是

串行化（serializable）              		   否         	否             		否

## 6.5 行锁，表锁

|        | MyISAM                                                   | InnoDB                                                    |
| ------ | -------------------------------------------------------- | --------------------------------------------------------- |
| 行表锁 | 表锁，即使操作一条记录也会锁住整个表，不适合高并发的操作 | 行锁,操作时只锁某一行，不对其它行有影响，适合高并发的操作 |

## 6.6 索引

**数据结构：B+Tree**

一般来说能够达到range就可以算是优化了

**口诀：**

全值匹配我最爱，最左前缀要遵守；

带头大哥不能死，中间兄弟不能断；

索引列上少计算，范围之后全失效；

LIKE百分写最右，覆盖索引不写*；

不等空值还有OR，索引影响要注意；

VAR引号不可丢，SQL优化有诀窍。

## 6.7 b-tree和b+tree的区别

（1）非叶子节点只存储键值信息

（2）所有叶子节点之间都有一个链指针

（3）数据记录都存放在叶子节点中

## 6.8 简述在MySQL数据库中MyISAM和InnoDB的区别

**InnoDB	存储引擎**

主要面向OLTP(Online Transaction Processing，在线事务处理)方面的应用

**特点：**

行锁设计、支持外键；

**MyISAM	存储引擎**

主要面向OLAP(Online Analytical Processing,在线分析处理)方面的应用。

**特点：**

不支持事务，支持表锁和全文索引。操作速度快。

## 6.9 你们公司有哪些数据库设计规范

**（一）基础规范**

1、表存储引擎必须使用InnoDB，表字符集默认使用utf8，必要时候使用utf8mb4

解读：

（1）通用，无乱码风险，汉字3字节，英文1字节

（2）utf8mb4是utf8的超集，有存储4字节例如表情符号时，使用它

2、禁止使用存储过程，视图，触发器，Event

解读：

（1）对数据库性能影响较大，互联网业务，能让站点层和服务层干的事情，不要交到数据库层

（2）调试，排错，迁移都比较困难，扩展性较差

3、禁止在数据库中存储大文件，例如照片，可以将大文件存储在对象存储系统，数据库中存储路径

4、禁止在线上环境做数据库压力测试

5、测试，开发，线上数据库环境必须隔离

**（二）命名规范**

1、库名，表名，列名必须用小写，采用下划线分隔

解读：abc，Abc，ABC都是给自己埋坑

2、库名，表名，列名必须见名知义，长度不要超过32字符

解读：tmp，wushan谁知道这些库是干嘛的

3、库备份必须以bak为前缀，以日期为后缀

4、从库必须以-s为后缀

5、备库必须以-ss为后缀

**（三）表设计规范**

1、单实例表个数必须控制在2000个以内

2、单表分表个数必须控制在1024个以内

3、表必须有主键，推荐使用UNSIGNED整数为主键

潜在坑：删除无主键的表，如果是row模式的主从架构，从库会挂住

4、禁止使用外键，如果要保证完整性，应由应用程式实现

解读：外键使得表之间相互耦合，影响update/delete等SQL性能，有可能造成死锁，高并发情况下容易成为数据库瓶颈

5、建议将大字段，访问频度低的字段拆分到单独的表中存储，分离冷热数据

**（四）列设计规范**

1、根据业务区分使用tinyint/int/bigint，分别会占用1/4/8字节

2、根据业务区分使用char/varchar

解读：

（1）字段长度固定，或者长度近似的业务场景，适合使用char，能够减少碎片，查询性能高

（2）字段长度相差较大，或者更新较少的业务场景，适合使用varchar，能够减少空间

3、根据业务区分使用datetime/timestamp

解读：前者占用5个字节，后者占用4个字节，存储年使用YEAR，存储日期使用DATE，存储时间使用datetime

4、必须把字段定义为NOT NULL并设默认值

解读：

（1）NULL的列使用索引，索引统计，值都更加复杂，MySQL更难优化

（2）NULL需要更多的存储空间

（3）NULL只能采用IS NULL或者IS NOT NULL，而在=/!=/in/not in时有大坑

5、使用INT UNSIGNED存储IPv4，不要用char(15)

6、使用varchar(20)存储手机号，不要使用整数

解读：

（1）牵扯到国家代号，可能出现+/-/()等字符，例如+86

（2）手机号不会用来做数学运算

（3）varchar可以模糊查询，例如like ‘138%’

7、使用TINYINT来代替ENUM

解读：ENUM增加新值要进行DDL操作

**（五）索引规范**

1、唯一索引使用uniq_[字段名]来命名

2、非唯一索引使用idx_[字段名]来命名

3、单张表索引数量建议控制在5个以内

解读：

（1）互联网高并发业务，太多索引会影响写性能

（2）生成执行计划时，如果索引太多，会降低性能，并可能导致MySQL选择不到最优索引

（3）异常复杂的查询需求，可以选择ES等更为适合的方式存储

4、组合索引字段数不建议超过5个

解读：如果5个字段还不能极大缩小row范围，八成是设计有问题

5、不建议在频繁更新的字段上建立索引

6、非必要不要进行JOIN查询，如果要进行JOIN查询，被JOIN的字段必须类型相同，并建立索引

解读：踩过因为JOIN字段类型不一致，而导致全表扫描的坑么？

7、理解组合索引最左前缀原则，避免重复建设索引，如果建立了(a,b,c)，相当于建立了(a), (a,b), (a,b,c)

**（六）SQL	规范**

1、禁止使用select *，只获取必要字段

解读：

（1）select *会增加cpu/io/内存/带宽的消耗

（2）指定字段能有效利用索引覆盖

（3）指定字段查询，在表结构变更时，能保证对应用程序无影响

2、insert必须指定字段，禁止使用insert into T values()

解读：指定字段插入，在表结构变更时，能保证对应用程序无影响

3、隐式类型转换会使索引失效，导致全表扫描

4、禁止在where条件列使用函数或者表达式

解读：导致不能命中索引，全表扫描

5、禁止负向查询以及%开头的模糊查询

解读：导致不能命中索引，全表扫描

6、禁止大表JOIN和子查询

7、同一个字段上的OR必须改写为IN，IN的值必须少于50个

8、应用程序必须捕获SQL异常

解读：方便定位线上问题

说明：本规范适用于并发量大，数据量大的典型互联网业务，可直接参考。

## 6.10 MySQL性能优化

（1）尽量选择较小的列

（2）将where中用的比较频繁的字段建立索引

（3）select子句中避免使用‘*’

（4）避免在索引列上使用计算、not in 和<>等操作

（5）当只需要一行数据的时候使用limit 1

（6）保证单表数据不超过200W，适时分割表。针对查询较慢的语句，可以使用explain 来分析该语句具体的执行情况。

（7）避免改变索引列的类型。

（8）选择最有效的表名顺序，from字句中写在最后的表是基础表，将被最先处理，在from子句中包含多个表的情况下，你必须选择记录条数最少的表作为基础表。

（9）避免在索引列上面进行计算。

（10）尽量缩小子查询的结果

## 6.11 SQL 语句优化案例

**例1：where** **子句中可以对字段进行 null** **值判断吗？**

可以，比如 select id from t where num is null 这样的 sql 也是可以的。但是最好不要给数据库留NULL，尽可能的使用 NOT NULL 填充数据库。不要以为 NULL 不需要空间，比如：char(100) 型，在字段建立时，空间就固定了， 不管是否插入值（NULL 也包含在内），都是占用 100 个字符的空间的，如果是 varchar 这样的变长字段，null 不占用空间。可以在 num 上设置默认值 0，确保表中 num 列没有 null 值，然后这样查询：select id from t where num= 0。

**例2：如何优化?下面的语句？**

select * from admin left join log on admin.admin_id = log.admin_id where log.admin_id>10

优化为：select * from (select * from admin where admin_id>10) T1 lef join log on T1.admin_id = log.admin_id。

使用 JOIN 时候，应该用小的结果驱动大的结果（left join 左边表结果尽量小如果有条件应该放到左边先处理， right join 同理反向），同时尽量把牵涉到多表联合的查询拆分多个 query（多个连表查询效率低，容易导致锁表和阻塞）。

**例3：limit 的基数比较大时使用 between**

例如：select * from admin order by admin_id limit 100000,10

优化为：select * from admin where admin_id between 100000 and 100010 order by admin_id。

**例4：尽量避免在列上做运算，这样导致索引失效**

例如：select * from admin where year(admin_time)>2014

优化为： select * from admin where admin_time> ‘2014-01-01′

## 6.12 常见面试sql

**例1：**

用一条SQL语句查询出每门课都大于80分的学生姓名

name    kecheng  fenshu
张三    语文    81
张三    数学    75
李四    语文    76
李四    数学   90
王五    语文    81
王五    数学    100
王五    英语    90

**答1：**

select distinct name from table where name not **in** **(**select distinct name from table where fenshu**<**=80**)**  

**答2：**

select name from table group by name having min**(**fenshu**)>**80  

**例2：**

学生表 如下:
自动编号    学号    姓名    课程编号    课程名称    分数
1             2005001 张三    0001       数学       69
2             2005002 李四    0001       数学       89
3             2005001 张三    0001       数学       69
删除除了自动编号不同，其他都相同的学生冗余信息
**答：**

delete tablename where 自动编号 not **in (**select min**(**自动编号**)** from tablename group by学号, 姓名, 课程编号, 课程名称, 分数**)**  

**例3：**

一个叫team的表，里面只有一个字段name,一共有4条纪录，分别是a,b,c,d,对应四个球队，现在四个球队进行比赛，用一条sql语句显示所有可能的比赛组合.

**答：**

select a.name, b.name  

from team a, team b   

where a.name **<** b.name  

**例4：**

怎么把这样一个表
year    month   amount
1991    1       		1.1
1991    2       		1.2
1991    3       		1.3
1991    4       		1.4
1992    1       		2.1
1992    2      		 2.2
1992    3       		2.3
1992    4       		2.4
查成这样一个结果
year    m1     m2     m3     m4
1991    1.1     1.2     1.3     1.4
1992    2.1     2.2     2.3     2.4 
**答：**

select year,   

**(**select amount from aaa m where month=1 and m.year=aaa.year**)** as m1,  

**(**select amount from aaa m where month=2 and m.year=aaa.year**)** as m2,  

**(**select amount from aaa m where month=3 and m.year=aaa.year**)** as m3,  

**(**select amount from  aaa m where month=4 and m.year=aaa.year**)** as m4  

from aaa group by year  
**例5：**

说明：复制表(只复制结构,源表名：a新表名：b) 

**答：**
SQL:

select ***** into b from a where 1**<>**1 **(**where1=1，拷贝表结构和数据内容**)**  

ORACLE:

 create table b  

As  

Select ***** from a where 1=2  

[<>（不等于）(SQL Server Compact)

比较两个表达式。 当使用此运算符比较非空表达式时，如果左操作数不等于右操作数，则结果为 TRUE。 否则，结果为 FALSE。]

**例6：**

原表：
courseid coursename   score
1       java            70
2       oracle       90
3       xml            40
4       jsp         30
5       servlet      80

为了便于阅读,查询此表后的结果显式如下(及格分数为60):
courseid coursename   score    mark
1       java            70      pass
2       oracle       90      pass
3       xml            40      fail
4       jsp         30      fail
5       servlet      80      pass
写出此查询语句

**答：**

select courseid, coursename ,score ,**if (score>=60, "pass","fail")**  as mark from course  

**例7：**

表名：购物信息

购物人  商品名称    数量

A      甲         2

B      乙    	 4

C      丙     	1

A      丁     	2

B      丙     	5

给出所有购入商品为两种或两种以上的购物人记录

**答：**

select ***** from 购物信息 where 购物人 **in** **(**select 购物人 from 购物信息 group by 购物人 having count**(*****)** **>**= 2**)**;  

**例8：**

info 表

date            result

2005-05-09   win

2005-05-09   lose

2005-05-09   lose

2005-05-09   lose

2005-05-10   win

2005-05-10   lose

2005-05-10   lose

如果要生成下列结果, 该如何写sql语句?

date            win     lose

2005-05-09     2      2

2005-05-10     1      2

**答1：**

select date, sum**(**case when result = "win" **then** 1 **else** 0 **end)** as "win", sum**(**case when result = "lose" **then** 1 **else** 0 **end)** as "lose" from info group by date;   

**答2：**

select a.date, a.result as win, b.result as lose   

from   

**(**select date, count**(**result**)** as result from info where result = "win" group by date**)** as a   

join   

**(**select date, count**(**result**)** as result from info where result = "lose" group by date**)** as b   

on a.date = b.date;  

## 7. Java Web

## 7.1 http 的长连接和短连接

HTTP 协议有 HTTP/1.0 版本和 HTTP/1.1 版本。HTTP1.1 默认保持长连接（HTTP persistent connection，也翻译为持久连接），数据传输完成了保持 TCP 连接不断开（不发 RST 包、不四次握手），等待在同域名下继续用这个通道传输数据；相反的就是短连接。

在 HTTP/1.0 中，默认使用的是短连接。也就是说，浏览器和服务器每进行一次 HTTP 操作，就建立一次连接，任务结束就中断连接。从 HTTP/1.1 起，默认使用的是长连接，用以保持连接特性。

## 7.2 http 常见的状态码有哪些？

200 OK  //客户端请求成功

301 Moved Permanently（永久移除)，请求的 URL 已移走。Response 中应该包含一个 Location URL, 说明资源现在所处的位置

302 found 重定向

400 Bad Request //客户端请求有语法错误，不能被服务器所理解

401 Unauthorized //请求未经授权，这个状态代码必须和 WWW-Authenticate 报头域一起使用

403 Forbidden //服务器收到请求，但是拒绝提供服务

404 Not Found //请求资源不存在，eg：输入了错误的 URL

500 Internal Server Error //服务器发生不可预期的错误

503 Server Unavailable //服务器当前不能处理客户端的请求，一段时间后可能恢复正常

## 7.3 GET 和POST 的区别？

（1）GET 请求的数据会附在URL 之后（就是把数据放置在 HTTP 协议头中），以?分割URL 和传输数据，参数之间以&相连，如：login.action?name=zhagnsan&password=123456。POST 把提交的数据则放置在是 HTTP 包的包体中。

（2）GET 方式提交的数据最多只能是 1024 字节，理论上POST 没有限制，可传较大量的数据。其实这样说是错误的，不准确的：“GET 方式提交的数据最多只能是 1024 字节”，因为 GET 是通过 URL 提交数据，那么 GET 可提交的数据量就跟URL 的长度有直接关系了。而实际上，URL 不存在参数上限的问题，HTTP 协议规范没有对 URL 长度进行限制。这个限制是特定的浏览器及服务器对它的限制。IE 对URL 长度的限制是2083 字节(2K+35)。对于其他浏览器，如Netscape、FireFox 等，理论上没有长度限制，其限制取决于操作系统的支持。

（3）POST 的安全性要比GET 的安全性高。注意：这里所说的安全性和上面 GET 提到的“安全”不是同个概念。上面“安全”的含义仅仅是不作数据修改，而这里安全的含义是真正的 Security 的含义，比如：通过 GET 提交数据，用户名和密码将明文出现在 URL 上，因为(1)登录页面有可能被浏览器缓存，(2)其他人查看浏览器的历史纪录，那么别人就可以拿到你的账号和密码了，除此之外，使用 GET 提交数据还可能会造成 Cross-site request forgery 攻击。

Get 是向服务器发索取数据的一种请求，而 Post 是向服务器提交数据的一种请求，在 FORM（表单）中，Method

默认为”GET”，实质上，GET 和 POST 只是发送机制不同，并不是一个取一个发！

## 7.4 Cookie 和Session 的区别

Cookie 是 web 服务器发送给浏览器的一块信息，浏览器会在本地一个文件中给每个 web 服务器存储 cookie。以后浏览器再给特定的 web 服务器发送请求时，同时会发送所有为该服务器存储的 cookie。

Session 是存储在 web 服务器端的一块信息。session 对象存储特定用户会话所需的属性及配置信息。当用户在应用程序的 Web 页之间跳转时，存储在 Session 对象中的变量将不会丢失，而是在整个用户会话中一直存在下去。

Cookie 和session 的不同点：

（1）无论客户端做怎样的设置，session 都能够正常工作。当客户端禁用 cookie 时将无法使用 cookie。

（2）在存储的数据量方面：session 能够存储任意的java 对象，cookie 只能存储 String 类型的对象。

## 7.5 在单点登录中，如果 cookie 被禁用了怎么办？

单点登录的原理是后端生成一个 session ID，然后设置到 cookie，后面的所有请求浏览器都会带上 cookie， 然后服务端从 cookie 里获取 session ID，再查询到用户信息。所以，保持登录的关键不是 cookie，而是通过cookie 保存和传输的 session ID，其本质是能获取用户信息的数据。除了 cookie，还通常使用 HTTP 请求头来传输。但是这个请求头浏览器不会像 cookie 一样自动携带，需要手工处理。

## 7.6 什么是jsp，什么是Servlet？jsp 和Servlet 有什么区别？

jsp 本质上就是一个Servlet，它是 Servlet 的一种特殊形式（由 SUN 公司推出），每个 jsp 页面都是一个servlet实例。

Servlet 是由 Java 提供用于开发 web 服务器应用程序的一个组件，运行在服务端，由 servlet 容器管理，用来生成动态内容。一个 servlet 实例是实现了特殊接口 Servlet 的 Java 类，所有自定义的 servlet 均必须实现 Servlet 接口。

**区别：**

jsp 是 html 页面中内嵌的Java 代码，侧重页面显示；

Servlet 是 html 代码和 Java 代码分离，侧重逻辑控制，mvc 设计思想中jsp 位于视图层，servlet 位于控制层

Jsp 运行机制：如下图

![img](http://www.atguigu.com/wp-content/uploads/image030.jpg)

JVM 只能识别 Java 类，并不能识别 jsp 代码！web 容器收到以.jsp 为扩展名的 url 请求时，会将访问请求交给tomcat 中 jsp 引擎处理，每个 jsp 页面第一次被访问时，jsp 引擎将 jsp 代码解释为一个 servlet 源程序，接着编译servlet 源程序生成.class 文件，再web 容器 servlet 引擎去装载执行servlet 程序，实现页面交互。

## 7.7 servlet生命周期

Servlet 加载—>实例化—>服务—>销毁。

**生命周期详解：**

**init（）：**

在Servlet的生命周期中，仅执行一次init()方法。它是在服务器装入Servlet时执行的，负责初始化Servlet对象。可以配置服务器，以在启动服务器或客户机首次访问Servlet时装入Servlet。无论有多少客户机访问Servlet，都不会重复执行init（）。

**service（）：**

它是Servlet的核心，负责响应客户的请求。每当一个客户请求一个HttpServlet对象，该对象的Service()方法就要调用，而且传递给这个方法一个“请求”（ServletRequest）对象和一个“响应”（ServletResponse）对象作为参数。在HttpServlet中已存在Service()方法。默认的服务功能是调用与HTTP请求的方法相应的do功能。

**destroy（）：**

仅执行一次，在服务器端停止且卸载Servlet时执行该方法。当Servlet对象退出生命周期时，负责释放占用的资源。一个Servlet在运行service()方法时可能会产生其他的线程，因此需要确认在调用destroy()方法时，这些线程已经终止或完成。

**如何与Tomcat** **结合工作步骤：**

（1）Web Client 向Servlet容器（Tomcat）发出Http请求

（2）Servlet容器接收Web Client的请求

（3）Servlet容器创建一个HttpRequest对象，将Web Client请求的信息封装到这个对象中。

（4）Servlet容器创建一个HttpResponse对象

（5）Servlet容器调用HttpServlet对象的service方法，把HttpRequest对象与HttpResponse对象作为参数传给HttpServlet 对象。

（6）HttpServlet调用HttpRequest对象的有关方法，获取Http请求信息。

（7）HttpServlet调用HttpResponse对象的有关方法，生成响应数据。

## 7.8 servlet特性

单例多线程

## 7.9 servlet是单实例的吗？

servlet是单实例的

## 7.10 servlet是线程安全的吗？为什么？

Servlet对象并不是一个线程安全的对象。

Servlet第一次被调用的时候，init()方法会被调用，然后调用service() 方法，从第二次被请求开始，就直接调用service()方法。

因为servlet是单实例的，所以后面再次请求同一个Servlet的时候都不会创建Servlet实例，

而且web容器会针对每个请求创建一个独立的线程，这样多个并发请求会导致多个线程同时调用 service() 方法，这样就会存在线程不安全的问题。

## 7.11 如何解决Servlet线程不安全的问题？

（1）不要在servlet中使用成员变量。

（2）可以给servlet中的方法添加同步锁，Synchronized，但是不提倡，数据并发访问会造成阻塞等待。

（3）可以实现 SingleThreadModel 接口，如下。这样可以避免使用成员变量的问题，但是也不提倡，原因同上。

Public class Servlet1 extends HttpServlet implements SingleThreadModel{

……..

}

## 7.12 谈谈过滤器的作用

过滤器，是在java web中，你传入的request,response提前过滤掉一些信息，或者提前设置一些参数，然后再传入servlet或者struts的 action进行业务逻辑，比如过滤掉非法url（不是login.do的地址请求，如果用户没有登陆都过滤掉）,或者在传入servlet或者 struts的action前统一设置字符集，或者去除掉一些非法字符 

## 7.13 谈谈拦截器的作用

拦截器，是在面向切面编程的就是在你的service或者一个方法，前调用一个方法，或者在方法后调用一个方法比如动态代理就是拦截器的简单实现，在你调用方法前打印出字符串（或者做其它业务逻辑的操作），也可以在你调用方法后打印出字符串，甚至在你抛出异常的时候做业务逻辑的操作。

## 7.14 拦截器和过滤器有什么区别

拦截器基于反射机制，而过滤器基于函数回调
拦截器基于Strust2或SpringMVC这样的表述层框架，而过滤器基于Servlet容器
拦截器只能在框架内部生效，而过滤器可以对所有请求生效
拦截器可以访问框架内的资源对象（例如Spring IOC容器中的对象），而过滤器不能直接访问框架内的资源对象

## 7.15 拦截器和过滤器的执行顺序

过滤前 – 拦截前 – Action处理 – 拦截后 – 过滤后。

过滤是一个横向的过程，首先把客户端提交的内容进行过滤(例如未登录用户不能访问内部页面的处理)；过滤通过后，拦截器将检查用户提交数据的验证，做一些前期的数据处理，接着把处理后的数据发给对应的Action；Action处理完成返回后，拦截器还可以做其他过程(还没想到要做啥)，再向上返回到过滤器的后续操作。

## 8. SSM

## 8.1 请写出 spring 中常用的依赖注入方式。

通过 setter 方法注入

通过构造方法注入

## 8.2 简述Spring中IOC容器常用的接口和具体的实现类

- ● BeanFactory SpringIOC容器的基本设置，是最底层的实现， 面向框架本身的. 
- ● ApplicationContext BeanFactory的子接口, 提供了更多高级的特定. 面向开发者的.
- ● ConfigurableApplicationContext, ApplicationContext的子接口，扩展出了 close 和 refresh等 关闭 刷新容器的方法
- ● ClassPathXmlApplicationContext：从classpath的XML配置文件中读取上下文，并生成上下文定义。应用程序上下文从程序环境变量中取得。
- ● FileSystemXmlApplicationContext ：由文件系统中的XML配置文件读取上下文。
- ● XmlWebApplicationContext：由Web应用的XML文件读取上下文。

## 8.3 简述Spring中如何基于注解配置Bean和装配Bean,

（1）首先要在Spring中配置开启注解扫描

```java
<context:component-scan base-package=” ”></ context:component-scan>
```

（2）在具体的类上加上具体的注解

（3）Spring 中通常使用@Autowired 或者是@Resource 等注解进行bean的装配

## 8.4 说出Spring 或者 Springmvc中常用的5个注解，并解释含义

@Component 基本注解，标识一个受Spring管理的组件

@Controller  标识为一个表示层的组件

@Service    标识为一个业务层的组件

@Repository  标识为一个持久层的组件

@Autowired   自动装配

@Qualifier(“”)  具体指定要装配的组件的id值

@RequestMapping() 完成请求映射

@PathVariable  映射请求URL中占位符到请求处理方法的形参

只要说出机几个注解并解释含义即可，如上答案只做参考

## 8.5 请解释Spring Bean的生命周期？

（1）默认情况下，IOC容器中bean的生命周期分为五个阶段:

​	● 调用构造器 或者是通过工厂的方式创建Bean对象

​	● bean对象的属性注入值

​	● 调用初始化方法，进行初始化，初始化方法是通过init-method来指定的.

​	● 使用

​	● IOC容器关闭时， 销毁Bean对象.

（2）当加入了Bean的后置处理器后，IOC容器中bean的生命周期分为七个阶段:

​	● 调用构造器 或者是通过工厂的方式创建Bean对象

​	● 给bean对象的属性注入值

​	● 执行Bean后置处理器中的 postProcessBeforeInitialization

​	● 调用初始化方法，进行初始化，初始化方法是通过init-method来指定的.

​	● 执行Bean的后置处理器中 postProcessAfterInitialization  

​	● 使用

​	● IOC容器关闭时， 销毁Bean对象

​	只需要回答出第一点即可，第二点也回答可适当 加分。

## 8.6 简单的谈一下SpringMVC的工作流程？

​	● 用户发送请求至前端控制器DispatcherServlet

​	● DispatcherServlet收到请求调用HandlerMapping处理器映射器。

​	● 处理器映射器找到具体的处理器，生成处理器对象及处理器拦截器(如果有则生成)一并返回给DispatcherServlet。

​	● DispatcherServlet调用HandlerAdapter处理器适配器

​	● HandlerAdapter经过适配调用具体的处理器(Controller，也叫后端控制器)。

​	● Controller执行完成返回ModelAndView

​	● HandlerAdapter将controller执行结果ModelAndView返回给DispatcherServlet

​	● DispatcherServlet将ModelAndView传给ViewReslover视图解析器

​	● ViewReslover解析后返回具体View

​	● DispatcherServlet根据View进行渲染视图（即将模型数据填充至视图中）。

​	● DispatcherServlet响应用户

## 8.7 SpringMVC中如何解决POST请求中文乱码问题

Springmvc中通过CharacterEncodingFilter解决中文乱码问题.

在web.xml中加入：

```java
<filter>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>  
    <init-param>  
        <param-name>encoding</param-name>  
        <param-value>utf-8</param-value>  
    </init-param>  
</filter>  
<filter-mapping>  
    <filter-name>CharacterEncodingFilter</filter-name>  
    <url-pattern>/*</url-pattern>  
</filter-mapping>  
```



## 8.8 简述SpringMvc里面拦截器是如何定义，如何配置，拦截器中三个重要的方法

**定义：**有两种方式

​	● 实现HandlerInterceptor接口

​	● 继承HandlerInterceptorAdapter

**配置：**

```java
<mvc:interceptors>  
    <!--默认是对所有请求都拦截 -->  
    <bean id="myFirstInterceptor" class="com.atguigu.interceptor.MyFirstInterceptor">  
    </bean>  
    <!-- 只针对部分请求拦截或者不拦截 -->  
    <mvc:interceptor>  
        <mvc:mapping path=" " />  <!—指定拦截-->  
        <mvc:exclude-mapping path=””/> <!—指定不拦截-->  
        <bean class=" com.atguigu.interceptor.MySecondInterceptor " /> </mvc:interceptor> 
</mvc:interceptors>  
```

**拦截器中三个重要的方法：**

​	● preHandle

​	● postHandle

​	● afterCompletion

## 8.9 MyBatis中 #{}和${}的区别是什么？

\#{}是预编译处理，${}是字符串替换；

Mybatis在处理#{}时，会将sql中的#{}替换为?号，调用PreparedStatement的set方法来赋值；

Mybatis在处理${}时，就是把${}替换成变量的值；

使用#{}可以有效的防止SQL注入，提高系统安全性。

## 8.10 Mybatis 结果集的映射方式有几种，并分别解释每种映射方式如何使用。

自动映射 ，通过resultType来指定要映射的类型即可。

自定义映射 通过resultMap来完成具体的映射规则，指定将结果集中的哪个列映射到对象的哪个属性。

## 8.11 简述MyBatis的单个参数、多个参数如何传递及如何取值。

MyBatis传递单个参数，如果是普通类型(String+8个基本)的，取值时在#{}中可以任意指定，如果是对象类型的，则在#{}中使用对象的属性名来取值

MyBatis传递多个参数，默认情况下，MyBatis会对多个参数进行封装Map，取值时在#{}可以使用0 1 2 .. 或者是param1 param2..

MyBatis传递多个参数，建议使用命名参数，在Mapper接口的方法的形参前面使用

@Param() 来指定封装Map时用的key. 取值时在#{}中使用@Param指定的key

## 8.12 MyBatis如何获取自动生成的(主)键值?

在<insert>标签中使用 useGeneratedKeys  和  keyProperty 两个属性来获取自动生成的主键值。

示例:

```java
<insert id=”insertname” usegeneratedkeys=”true” keyproperty=”id”>  
    insert into names (name) values (#{name})  
</insert>  
```



## 述Mybatis的动态SQL，列出常用的6个标签及作用

动态SQL是MyBatis的强大特性之一 基于功能强大的OGNL表达式。

动态SQL主要是来解决查询条件不确定的情况，在程序运行期间，根据提交的条件动态的完成查询

常用的标签:

<if> : 进行条件的判断

<where>：在<if>判断后的SQL语句前面添加WHERE关键字，并处理SQL语句开始位置的AND 或者OR的问题

<trim>：可以在SQL语句前后进行添加指定字符 或者去掉指定字符.

<set>: 主要用于修改操作时出现的逗号问题

<choose> <when> <otherwise>：类似于java中的switch语句.在所有的条件中选择其一

<foreach>：迭代操作

## 8.14 Mybatis的Xml映射文件中，不同的Xml映射文件，id是否可以重复？

不同的Xml映射文件，如果配置了namespace，那么id可以重复；如果没有配置namespace，那么id不能重复。

## 8.15 Mybatis 如何完成MySQL的批量操作,举例说明

MyBatis完成MySQL的批量操作主要是通过<foreach>标签来拼装相应的SQL语句.

例如:

```java
<insert id="insertBatch" >  
    insert into tbl_employee(last_name,email,gender,d_id) values  
    <foreach collection="emps" item="curr_emp" separator=",">  
        (#{curr_emp.lastName},#{curr_emp.email},#{curr_emp.gender},#{curr_emp.dept.id})  
    </foreach>  
</insert>  
```



## 8.16 简述Spring中如何给bean对象注入集合类型的属性

Spring使用 <list> <set> <map> 等标签给对应类型的集合注入值

## 8.17 简述Spring 中bean的作用域

总共有四种作用域:

- ● Singleton 单例的
- ● Prototype 原型的
- ● Request
- ● Session

## 8.18 简述Spring中自动装配常用的两种装配模式

byName: 根据bean对象的属性名进行装配

byType： 根据bean对象的属性的类型进行装配,需要注意匹配到多个兼容类型的bean对象时，会抛出异常。

## 8.19 请解释@Autowired注解的工作机制及required属性的作用

（1）首先会使用byType的方式进行自动装配，如果能唯一匹配，则装配成功，

如果匹配到多个兼容类型的bean, 还会尝试使用byName的方式进行唯一确定.

如果能唯一确定，则装配成功，如果不能唯一确定，则装配失败，抛出异常.

（2）默认情况下， 使用@Autowired标注的属性必须被装配，如果装配不了，也会抛出异常.

可以使用required=false来设置不是必须要被装配.

## 8.20 简述Springmvc中ContextLoaderListener的作用以及实现原理

**作用：**

ContextLoaderListener的作用是通过监听的方式在WEB应用服务器启动时将Spring的容器对象进行初始化.

**原理：**

ContextLoaderListener 实现了ServletContextListener接口，用于监听

ServletContext的创建，当监听到ServletContext创建时，在对应contextInitialized

方法中，将Spring的容器对象进行创建，并将创建好的容器对象设置到ServletContext域对象中，

目的是让各个组件可以通过ServletContext共享到Spring的容器对象

## 8.21 简述Mybatis提供的两级缓存，以及缓存的查找顺序

（1）MyBatis的缓存分为一级缓存和 二级缓存。

一级缓存是SqlSession级别的缓存，默认开启。

二级缓存是NameSpace级别(Mapper)的缓存，多个SqlSession可以共享，使用时需要进行配置开启。

（2）缓存的查找顺序：二级缓存 => 一级缓存 => 数据库

## 8.22 简述Spring与Springmvc整合时，如何解决bean被创建两次的问题

Bean被创建两次的问题是在组建扫描的配置中指定Springmvc只负责扫描WEB相关的组件，Spring扫描除了Springmvc之外的组件。

## 8.23 简述Spring与Mybatis整合时，主要整合的两个地方

（1）SqlSession创建的问题，通过SqlSessionFactoryBean来配置用于创建SqlSession的信息。例如: Mybatis的核心配置文件、Mapper映射文件、数据源等

（2）Mapper接口创建的问题， 使用MapperScannerConfigurer批量为MyBatis的Mapper接口生成代理实现类并将具体的对象交给Spring容器管理

## 8.24 简述Spring声明式事务中@Transaction中常用的两种事务传播行为

通过propagation来执行事务的传播行为

REQUIRED：使用调用者的事务，如果调用者没有事务，则启动新的事务运行

REQUIRES_NEW：将调用者的事务挂起，开启新的事务运行。

## 8.25 简述@RequestMapping注解的作用，可标注的位置，常用的属性

（1）该注解的作用是用来完成请求 与  请求处理方法的映射

（2）该注解可以标注在类上或者是方法上

（3）常用的属性:

value: 默认属性， 用于指定映射的请求URL

method: 指定映射的请求方式

params: 指定映射的请求参数

headers: 指定映射的请求头信息

## 8.26 简述Springmvc中处理模型数据的两种方式

- ● 使用ModelAndView 作为方法的返回值，将模型数据和视图信息封装到ModelAndView中
- ● 使用Map或者是Model 作为方法的形参，将模型数据添加到Map或者是Model中

## 8.27 简述REST中的四种请求方式及对应的操作

GET  查询操作

POST 添加操作

DELETE 删除操作

PUT  修改操作

## 8.28 简述视图和视图解析的关系及作用

- ● 视图是由视图解析器解析得到的。
- ● 视图解析器的作用是根据ModelAndView中的信息解析得到具体的视图对象
- ● 视图的作用是完成模型数据的渲染工作，最终完成转发或者是重定向的操作

## 8.29 说出三个 常用的视图类

InternalResourceView

JstlView

RedirectView

## 8.30 简述REST中HiddenHttpMethodFilter过滤器的作用

该过滤器主要负责转换客户端请求的方式，当浏览器的请求方式为POST，并且在请求中能通过 _method获取到请求参数值。该过滤器就会进行请求方式的转换。

一般在REST中，都是将POST请求转换为对应的DELETE 或者是PUT

## 8.31 简述Springmvc中如何返回JSON数据

Step1：在项目中加入json转换的依赖，例如jackson，fastjson，gson等

Step2：在请求处理方法中将返回值改为具体返回的数据的类型， 例如数据的集合类List<Employee>等

Step3：在请求处理方法上使用@ResponseBody注解

这里再补充一个注意点：使用@ResponseBody注解需要开启注解驱动功能，也就是需要配置

## 8.32 简述如何在myBatis中的增删改操作获取到对数据库的影响条数

直接在Mapper接口的方法中声明返回值即可

## 8.33 Springmvc中的控制器的注解用哪个，可以是否用别的注解代替

使用@Controller注解来标注控制器，不能使用别的注解代替。

## 8.34 如何在Springmvc中获取客户端提交的请求参数

直接在请求处理方法中声明对应的形参，也可以是用@RequestParam注解来具体指定将那些请求参数映射到方法中对应的形参。

## 8.35 简述Springmvc中InternalResourceViewResolver解析器的工作机制

使用prefix + 方法的返回值 + suffix 生成一个物理视图路径。

## 8.36 Springmvc中如何完成重定向

在请求处理方法的返回值前面加 redirect: 前缀, 最终会解析得到RedirectView，RedirectView会完成重定向的操作。

## 8.37 简述Spring中切面中常用的几种通知，并简单解释

前置通知  在目标方法执行之前执行

后置通知  在目标方法执行之后执行，不管目标方法有没有抛出异常

返回通知  在目标方法成功返回之后执行， 可以获取到目标方法的返回值

异常通知  在目标方法抛出异常后执行

环绕通知  环绕着目标方法执行

## 8.38 解释MyBatis中 @Param注解的作用

通过该注解来指定Mybatis底层在处理参数时封装Map使用的key，方便在SQL映射文件中取参数。

## 8.39 简述Mybatis中使用Mapper接口开发，如何完成Mapper接口与SQL映射文件、方法与SQL语句的绑定

Mapper接口与SQL映射文件绑定：SQL映射文件中的namespace的值指定成Mapper接口的全类名

接口中方法与SQL语句的绑定：SQL语句的id 指定成接口中的方法名。

## 8.40 SpringMVC的工作原理

（1）用户向服务器发送请求，请求被springMVC 前端控制器 DispatchServlet 捕获；

（2）DispatcherServle 对请求 URL 进行解析，得到请求资源标识符（URL），然后根据该 URL 调用 HandlerMapping将请求映射到处理器 HandlerExcutionChain；

（3）DispatchServlet 根据获得 Handler 选择一个合适的HandlerAdapter 适配器处理；

（4）Handler 对数据处理完成以后将返回一个 ModelAndView（）对象给 DisPatchServlet;

（5）Handler 返回的 ModelAndView() 只是一个逻辑视图并不是一个正式的视图， DispatcherSevlet 通过ViewResolver 试图解析器将逻辑视图转化为真正的视图View;

（6）DispatcherServle 通过 model 解析出 ModelAndView()中的参数进行解析最终展现出完整的 view 并返回给客户端;

![img](http://www.atguigu.com/wp-content/uploads/image032.jpg)

## 8.41 谈谈你对Spring 的理解

Spring 是一个开源框架，为简化企业级应用开发而生。Spring 可以是使简单的JavaBean 实现以前只有EJB 才能实现的功能。Spring 是一个 IOC 和 AOP 容器框架。

Spring 容器的主要核心是：

控制反转（IOC），传统的 java 开发模式中，当需要一个对象时，我们会自己使用 new 或者 getInstance 等直接或者间接调用构造方法创建一个对象。而在 spring 开发模式中，spring 容器使用了工厂模式为我们创建了所需要的对象，不需要我们自己创建了，直接调用spring 提供的对象就可以了，这是控制反转的思想。

依赖注入（DI），spring 使用 javaBean 对象的 set 方法或者带参数的构造方法为我们在创建所需对象时将其属性自动设置所需要的值的过程，就是依赖注入的思想。

面向切面编程（AOP），在面向对象编程（oop）思想中，我们将事物纵向抽成一个个的对象。而在面向切面编程中，我们将一个个的对象某些类似的方面横向抽成一个切面，对这个切面进行一些如权限控制、事物管理，记录日志等公用操作处理的过程就是面向切面编程的思想。AOP 底层是动态代理，如果是接口采用 JDK 动态代理，如果是类采用CGLIB 方式实现动态代理。

## 8.42 Spring中常用的设计模式

（1）代理模式——spring 中两种代理方式，若目标对象实现了若干接口，spring 使用jdk 的java.lang.reflect.Proxy类代理。若目标兑现没有实现任何接口，spring 使用 CGLIB 库生成目标类的子类。

（2）单例模式——在 spring 的配置文件中设置 bean 默认为单例模式。

（3）模板方式模式——用来解决代码重复的问题。

比如：RestTemplate、JmsTemplate、JpaTemplate

（4）工厂模式——在工厂模式中，我们在创建对象时不会对客户端暴露创建逻辑，并且是通过使用同一个接口来指向新创建的对象。Spring 中使用 beanFactory 来创建对象的实例。

## 8.43 请描述一下Spring的事务管理

（1）声明式事务管理的定义：用在 Spring 配置文件中声明式的处理事务来代替代码式的处理事务。这样的好处是，事务管理不侵入开发的组件，具体来说，业务逻辑对象就不会意识到正在事务管理之中，事实上也应该如此，因为事务管理是属于系统层面的服务，而不是业务逻辑的一部分，如果想要改变事务管理策划的话，也只需要在定义文件中重新配置即可，这样维护起来极其方便。

基于 TransactionInterceptor 的声明式事务管理：两个次要的属性： transactionManager，用来指定一个事务治理器， 并将具体事务相关的操作请托给它； 其他一个是 Properties 类型的transactionAttributes 属性，该属性的每一个键值对中，键指定的是方法名，方法名可以行使通配符， 而值就是表现呼应方法的所运用的事务属性。

（2）基于 @Transactional 的声明式事务管理：Spring 2.x 还引入了基于 Annotation 的体式格式，具体次要触及@Transactional 标注。@Transactional 可以浸染于接口、接口方法、类和类方法上。算作用于类上时，该类的一切public 方法将都具有该类型的事务属性。

（3）编程式事物管理的定义：在代码中显式挪用 beginTransaction()、commit()、rollback()等事务治理相关的方法， 这就是编程式事务管理。Spring 对事物的编程式管理有基于底层 API 的编程式管理和基于 TransactionTemplate 的编程式事务管理两种方式。

## 9. SpringBoot

## 9.1 什么是 Spring Boot？

Spring Boot 是 Spring 开源组织下的子项目，是 Spring 组件一站式解决方案，主要是简化了使用 Spring 的难度，简省了繁重的配置，提供了各种启动器，开发者能快速上手。

![微信图片_20190930113823](http://www.atguigu.com/wp-content/uploads/image034.jpg)

## 9.2 为什么要用 Spring Boot？

**Spring Boot 的优点**

● 独立运行

Spring Boot而且内嵌了各种servlet容器，Tomcat、Jetty等，现在不再需要打成war包部署到容器中，Spring Boot只要打成一个可执行的jar包就能独立运行，所有的依赖包都在一个jar包内。

● 简化配置

spring-boot-starter-web启动器自动依赖其他组件，简少了maven的配置。除此之外，还提供了各种启动器，开发者能快速上手。

● 自动配置

Spring Boot能根据当前类路径下的类、jar包来自动配置bean，如添加一个spring-boot-starter-web启动器就能拥有web的功能，无需其他配置。

● 无代码生成和XML配置

Spring Boot配置过程中无代码生成，也无需XML配置文件就能完成所有配置工作，这一切都是借助于条件注解完成的，这也是Spring4.x的核心功能之一。

● 应用监控

Spring Boot提供一系列端点可以监控服务及应用，做健康检测。

## 9.3 Spring Boot有哪些缺点？

Spring Boot虽然上手很容易，但如果你不了解其核心技术及流程，所以一旦遇到问题就很棘手，而且现在的解决方案也不是很多，需要一个完善的过程。

## 9.4 Spring Boot 的核心配置文件有哪几个？它们的区别是什么？

Spring Boot 的核心配置文件是 application 和 bootstrap 配置文件。

application 配置文件这个容易理解，主要用于 Spring Boot 项目的自动化配置。

**bootstrap 配置文件的特性：**

​	● boostrap 由父 ApplicationContext 加载，比 applicaton 优先加载

​	● boostrap 里面的属性不能被覆盖

**bootstrap** **配置文件有以下几个应用场景：**

​	● 使用 Spring Cloud Config 配置中心时，这时需要在 bootstrap 配置文件中添加连接到配置中心的配置属性来加载外部配置中心的配置信息；

​	● 一些固定的不能被覆盖的属性；

​	● 一些加密/解密的场景；

## 9.5 Spring Boot 的配置文件有哪几种格式？它们有什么区别？

.properties 和 .yml，它们的区别主要是书写格式不同。

1).properties

```java
app.user.name = javastack
```

2).yml

```
app:
  user:
    name: javastack
```



## 9.6 Spring Boot 的核心注解是哪个？它主要由哪几个注解组成的？

启动类上面的注解是@SpringBootApplication，它也是 Spring Boot 的核心注解，主要组合包含了以下 3 个注解：

-  @SpringBootConfiguration：组合了 @Configuration 注解，实现配置文件的功能。
-  @EnableAutoConfiguration：打开自动配置的功能，也可以关闭某个自动配置的选项，
   - 如关闭数据源自动配置功能： @SpringBootApplication(exclude = { DataSourceAutoConfiguration.class })。
-  @ComponentScan：Spring组件扫描。

## 9.7 开启 Spring Boot 特性有哪几种方式？

1. 继承spring-boot-starter-parent项目

```java
<parent>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-parent</artifactId>  
    <version> 2.0.7.RELEASE  </version>  
</parent>  
```

● 如果项目已经继承了其他父项目，则可以导入spring-boot-dependencies项目依赖

```java
<dependencyManagement>
    <dependencies>
        <!-- 导入SpringBoot需要使用的依赖信息 -->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.1.6.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```



## 9.8 Spring Boot 需要独立的容器运行吗？

可以不需要，内置了 Tomcat/ Jetty 等容器。

## 9.9 运行 Spring Boot 有哪几种方式？

1）打包命令或者放到容器中运行

2）用 Maven/ Gradle 插件运行

3）直接执行 main 方法运行

## 9.10 Spring Boot 自动配置原理是什么？

SpringBoot的自动化配置原理可以从以下7点介绍：
与自动化配置相关的jar包是spring-boot-autoconfigure-2.1.6.RELEASE.jar
在spring-boot-autoconfigure-2.1.6.RELEASE.jar这个jar包里有个META-INF目录
META-INF目录下有个spring.factories文件
spring.factories文件中有个配置项是org.springframework.boot.autoconfigure.EnableAutoConfiguration
这个配置项对应的值就是各个具体的自动化配置类
在具体的自动化配置类上有四个（组）相关注解
@Configuration注解表示当前类是一个“配置”类
@ConditionalOnXxx注解表示当前类需要满足指定条件才会加载到IOC容器中
@EnableConfigurationProperties注解用于加载XxxProperties类
@Import注解加载运行过程中用到的类
XxxProperties类
这个类中封装了当前starter范围内常用的自动化配置信息，例如整合Redis时使用的主机地址、端口号等等。有些有默认值。
SpringBoot会读取这个类中的数据作为默认配置。
这个类同时还指定了在application.properties或application.yml中针对当前starter可以使用的配置项。所以这个类其实是SpringBoot配置文件中配置项的依据。在application.properties或application.yml中所做的配置本质上是对XxxProperties类中默认值的覆盖。
XxxProperties类需要标记@ConfigurationProperties注解才能够被SpringBoot识别
@ConfigurationProperties注解通过prefix属性指定在application.properties或application.yml中做相关配置时使用的前缀

**11、你如何理解 Spring Boot 中的 Starters？**

SpringBoot的starter我们翻译成“场景启动器”，是SpringBoot的一个重要特色和优势。
在一个starter中SpringBoot不仅提供了这个场景下所需要的所有依赖包而且通过版本仲裁保证所引入的依赖包版本正确，最大限度降低了jar包冲突隐患。
不仅如此SpringBoot还在starter中封装了该场景在实际开发中总结出来的最佳实践，以自动化配置的形式把常用默认配置给我们直接配置好。例如我们在使用SpringMVC时需要配置mvc:annotation-driven开启注解驱动，在引入spring-boot-web-starter后就不需要了，注解支持已经作为最佳实践整合到了starter中。还有spring-boot-web-starter里面也加入了对JSON数据解析能力的支持，这在SpringMVC中是需要程序员自己引入相关jar包的。所以SpringBoot的starter几乎做到了想要的功能一键开启、自动运行。

**12、如何在 Spring Boot 启动的时候运行一些特定的代码？**

可以实现接口 ApplicationRunner 或者 CommandLineRunner，这两个接口实现方式一样，它们都只提供了一个 run 方法，实现上述接口的类加入IOC容器即可生效。

**13、Spring Boot 有哪几种读取配置的方式？**

Spring Boot 可以通过 @PropertySource,@Value,@Environment, @ConfigurationProperties 来绑定变量。

**14、Spring Boot 支持哪些日志框架？推荐和默认的日志框架是哪个？**

Spring Boot 支持 Java Util Logging, Log4j2, Lockback 作为日志框架，如果你使用 Starters 启动器，Spring Boot 将使用 Logback 作为默认日志框架。

**15、SpringBoot 实现热部署有哪几种方式？**

主要有两种方式：

Spring Loaded

Spring-boot-devtools

**16、你如何理解 Spring Boot 配置加载顺序？**

1、开发者工具 `Devtools` 全局配置参数；
2、单元测试上的 `@TestPropertySource` 注解指定的参数；
3、单元测试上的 `@SpringBootTest` 注解指定的参数；
4、命令行指定的参数，如 `java -jar springboot.jar --name="Java技术栈"`；
5、命令行中的 `SPRING_APPLICATION_JSONJSON` 指定参数, 如 `java -Dspring.application.json='{"name":"Java技术栈"}' -jar springboot.jar`
6、`ServletConfig` 初始化参数；
7、`ServletContext` 初始化参数；
8、JNDI参数（如 `java:comp/env/spring.application.json`）；
9、Java系统参数（来源：`System.getProperties()`）；
10、操作系统环境变量参数；
11、`RandomValuePropertySource` 随机数，仅匹配：`ramdom.*`；
12、JAR包外面的配置文件参数（`application-{profile}.properties（YAML）`）
13、JAR包里面的配置文件参数（`application-{profile}.properties（YAML）`）
14、JAR包外面的配置文件参数（`application.properties（YAML）`）
15、JAR包里面的配置文件参数（`application.properties（YAML）`）
16、`@Configuration`配置文件上 `@PropertySource` 注解加载的参数；
17、默认参数（通过 `SpringApplication.setDefaultProperties` 指定）；

数字越小优先级越高，即数字小的会覆盖数字大的参数值。

**17、Spring Boot 如何定义多套不同环境配置？**

开发阶段
基于properties配置文件
第一步
创建各环境对应的properties配置文件
applcation.properties
application-dev.properties
application-test.properties
application-prod.properties
第二步
然后在applcation.properties文件中指定当前的环境spring.profiles.active=test,这时候读取的就是application-test.properties文件。
基于yml配置文件
只需要一个applcation.yml文件就能搞定，推荐此方式。
spring:
profiles:

## active: prod

spring:
profiles: dev
server:

## port: 8080

spring:
profiles: test
server:

## port: 8081

spring.profiles: prod
spring.profiles.include:

- proddb
- prodmq
  server:

## port: 8082

spring:
profiles: proddb
db:

## name: mysql

spring:
profiles: prodmq
mq:
address: localhost
运行阶段指定profile
通过main方法启动
// 在Eclipse Arguments里面添加
–spring.profiles.active=prod
通过插件启动
spring-boot:run -Drun.profiles=prod
通过java -jar命令启动
java -jar xx.jar –spring.profiles.active=prod

## 9.18 Spring Boot 可以兼容老 Spring 项目吗，如何做？

可以兼容，使用 @ImportResource 注解导入老 Spring 项目配置文件。

## 9.19 Spring Boot 2.X 有什么新特性？与 1.X 有什么区别？

-  依赖 JDK 版本升级：2.x 里面的许多方法应用了 JDK 8 的许多高级新特性，至少需要 JDK 8 的支持；
-  第三方类库升：2.x 对第三方类库升级了所有能升级的稳定版本，例如：Spring Framework 5+、Tomcat 8.5+、Hibernate 5.2+、Thymeleaf 3+；
-  响应式 Spring 编程：2.x 通过启动器和自动配置全面支持 Spring 的响应式编程，响应式编程是完全异步和非阻塞的，它是基于事件驱动模型，而不是传统的线程模型；
-  连接池：2.x 默认使用 HikariCP 连接池；
-  json：提供了一个 spring-boot-starter-json 启动器对 JSON 读写的支持；
-  Quartz：2.x 提供了一个 spring-boot-starter-quartz 启动器对定时任务框架 Quartz 的支持；
-  HTTP/2 支持：提供对HTTP/2 的支持，如：Tomcat, Undertow, Jetty；
-  Actuator加强：在 2.x 中，对执行器端点进行了许多改进，所有的 HTTP 执行端点现在都暴露在 /actuator路径下，并对 JSON 结果集也做了改善。

## 10. SpringCloud

## 10.1 Spring Boot和Spring 是什么关系

SpringBoot底层就是Spring，简化使用Spring的方式而已，多加了好多的自动配置

## 10.2 Spring Boot和Spring Cloud是什么关系

Spring Boot 是 Spring 的一套快速配置脚手架，可以基于Spring Boot 快速开发单个微服务，Spring Cloud是一个基于Spring Boot实现的开发工具；Spring Boot专注于快速、方便集成的单个微服务个体，Spring Cloud关注全局的服务治理框架； Spring Boot使用了约定大于配置的理念，很多集成方案已经帮你选择好了，能不配置就不配置，Spring Cloud很大的一部分是基于Spring Boot来实现，必须基于Spring Boot开发。

 可以单独使用Spring Boot开发项目，但是Spring Cloud离不开 Spring Boot。

## 10.3 Eureka和zookeeper的区别

著名的CAP理论指出，一个分布式系统不可能同时满足C(一致性)、A(可用性)和P(分区容错性)。由于分区容错性在是分布式系统中必须要保证的，因此我们只能在A和C之间进行权衡。在此Zookeeper保证的是CP, 而Eureka则是AP。

**Zookeeper	保证CP**

当向注册中心查询服务列表时，我们可以容忍注册中心返回的是几分钟以前的注册信息，但不能接受服务直接down掉不可用。也就是说，服务注册功能对可用性的要求要高于一致性。但是zk会出现这样一种情况，当master节点因为网络故障与其他节点失去联系时，剩余节点会重新进行leader选举。问题在于，选举leader的时间太长，30 ~ 120s, 且选举期间整个zk集群都是不可用的，这就导致在选举期间注册服务瘫痪。在云部署的环境下，因网络问题使得zk集群失去master节点是较大概率会发生的事，虽然服务能够最终恢复，但是漫长的选举时间导致的注册长期不可用是不能容忍的。

**Eureka	保证AP**

Eureka看明白了这一点，因此在设计时就优先保证可用性。Eureka各个节点都是平等的，几个节点挂掉不会影响正常节点的工作，剩余的节点依然可以提供注册和查询服务。而Eureka的客户端在向某个Eureka注册或时如果发现连接失败，则会自动切换至其它节点，只要有一台Eureka还在，就能保证注册服务可用(保证可用性)，只不过查到的信息可能不是最新的(不保证强一致性)。除此之外，Eureka还有一种自我保护机制，如果在15分钟内超过85%的节点都没有正常的心跳，那么Eureka就认为客户端与注册中心出现了网络故障，此时会出现以下几种情况：

1. Eureka不再从注册列表中移除因为长时间没收到心跳而应该过期的服务

2. Eureka仍然能够接受新服务的注册和查询请求，但是不会被同步到其它节点上(即保证当前节点依然可用)

3. 当网络稳定时，当前实例新的注册信息会被同步到其它节点中

因此， Eureka可以很好的应对因网络故障导致部分节点失去联系的情况，而不会像zookeeper那样使整个注册服务瘫痪。

**总结**

Eureka作为单纯的服务注册中心来说要比zookeeper更加“专业”，因为注册服务更重要的是可用性，我们可以接受短期内达不到一致性的状况。不过Eureka目前1.X版本的实现是基于servlet的java web应用，它的极限性能肯定会受到影响。期待正在开发之中的2.X版本能够从servlet中独立出来成为单独可部署执行的服务。

## 11. Redis

## 11.1 什么是Redis？

Redis本质上是一个Key-Value类型的内存数据库，很像memcached，整个数据库统统加载在内存当中进行操作，定期通过异步操作把数据库数据flush到硬盘上进行保存。因为是纯内存操作，Redis的性能非常出色，每秒可以处理超过 10万次读写操作，是已知性能最快的Key-Value DB。 Redis的出色之处不仅仅是性能，Redis最大的魅力是支持保存多种数据结构，此外单个value的最大限制是1GB，不像 memcached只能保存1MB的数据，因此Redis可以用来实现很多有用的功能，比方说用他的List来做FIFO双向链表，实现一个轻量级的高性 能消息队列服务，用他的Set可以做高性能的tag系统等等。另外Redis也可以对存入的Key-Value设置expire时间，因此也可以被当作一 个功能加强版的memcached来用。 Redis的主要缺点是数据库容量受到物理内存的限制，不能用作海量数据的高性能读写，因此Redis适合的场景主要局限在较小数据量的高性能操作和运算上。

## 11.2 Redis的全称是什么？

Remote Dictionary Server

## 11.3 redis有哪些数据类型

| string            | 字符串                   |
| ----------------- | ------------------------ |
| list              | 可以重复的集合           |
| set               | 不可以重复的集合         |
| hash              | 类似于Map<String,String> |
| zset(sorted set） | 带分数的set              |

## 11.4 一个字符串类型的值能存储最大容量是多少？

512M

## 11.5 怎么理解Redis事务？

Redis无法做到像关系型数据库事务那样严格的ACID属性，特别是Redis官网明确指出了Redis为什么不支持回滚。

为了内部结构简单、运行效率更高，Redis舍弃了事务控制过程中的回滚支持。一个队列中的多个命令除非是在加入队列时发现错误会做到整个事务都不执行，否则所有命令都会执行，哪怕是队列中有的命令执行失败——显然Redis并没有在这里对队列中的多条命令进行回滚处理。Redis认为这些错误都应该在开发过程中被发现，而不是产品上线之后。

配合WATCH命令之后Redis的事务可以实现乐观锁效果：一个队列中的命令在执行时如果检测到碰撞，则放弃自己的操作。

## 11.6 Redis事务相关的命令有哪几个？

MULTI、EXEC、DISCARD、WATCH

## 11.7 Redis key的过期时间和永久有效分别怎么设置？

EXPIRE和PERSIST命令。

## 11.8 Redis持久化数据和缓存怎么做扩容？

如果Redis被当做缓存使用，使用一致性哈希实现动态扩容缩容。

如果Redis被当做一个持久化存储使用，必须使用固定的keys-to-nodes映射关系，节点的数量一旦确定不能变化。否则的话(即Redis节点需要动态变化的情况），必须使用可以在运行时进行数据再平衡的一套系统，而当前只有Redis集群可以做到这样。4、Redis主要消耗什么物理资源？

内存。

## 11.9 为什么Redis需要把所有数据放到内存中？

Redis为了达到最快的读写速度将数据都读到内存中，并通过异步的方式将数据写入磁盘。所以redis具有快速和数据持久化的特征。如果不将数据放在内存中，磁盘I/O速度为严重影响redis的性能。在内存越来越便宜的今天，redis将会越来越受欢迎。 如果设置了最大使用的内存，则数据已有记录数达到内存限值后不能继续插入新值。

## 11.10 Redis如何做内存优化？

尽可能使用散列表（hashes），散列表（是说散列表里面存储的数少）使用的内存非常小，所以你应该尽可能的将你的数据模型抽象到一个散列表里面。比如你的web系统中有一个用户对象，不要为这个用户的名称，姓氏，邮箱，密码设置单独的key,而是应该把这个用户的所有信息存储到一张散列表里面.

## 11.11 缓存穿透

**缓存系统定义：**

按照KEY去查询VALUE，当KEY对应的VALUE一定不存在的时候并对KEY并发请求量很大的时候，就会对后端造成很大的压力。（查询一个必然不存在的数据。比如文章表，查询一个不存在的id，每次都会访问DB，如果有人恶意破坏，很可能直接对DB造成影响。）

由于缓存不命中，每次都要查询持久层。从而失去缓存的意义。

**解决方法：**

（1）缓存层缓 存空值。

缓存太多空值，占用更多空间。（优化：给个空值过 期时间）

存储层更新代码了，缓存层还是空值。（优化：后台设置时主动删除空值，并缓存把值进去）

（2）将数据库中所有的查询条件，放布隆过滤器中。当一个查询请求来临的时候，先经过布隆过滤器进行查，如果请求存在这个条件中，那么继续执行，如果不在，直接丢弃。

**备注** **：**

比如数据库中有10000个条件，那么布隆过滤器的容量size设置的要稍微比10000大一些，比如12000.

对于误判率的设置，根据实际项目，以及硬件设施来具体定。但一定不能设置为0，并且误判率设置的越小，哈希函数跟数组长度都会更多跟更长，那么对硬件，内存中间的要求就会相应 的高

private st atic BloomFilter<Inte ger> bloomFi lt er = BloomFilter.create(Funnels.integerFue l(), s ize, 000 01) ;

有了siz跟误判率，那么布隆过滤器会产相应的哈希函数跟数组。 

综上：我们可以利用布隆过滤器，将redis缓存击穿制在一个可容的范围内。

## 11.12 哨兵模式

如果Master异常，则会进行Master-Slave切换，将其中一Slae作为Master，将之前的Master作为Slave

**下线：**

①主观下线：Subjectively Down，简称 SDOWN，指的是当前 Sentinel 实例对某个redis服务器做出的下线判断。

②客观下线：Objectively Down， 简称 ODOWN，指的是多个 Sentinel 实例在对Master Server做出 SDOWN 判断，并且通过 SENTINEL is-master-down-by-addr 命令互相交流之后，得出的Master Server下线判断，然后开启failover.

**工作原理：**

（1）每个Sentinel以每秒钟一次的频率向它所知的Master，Slave以及其他 Sentinel 实例发送一个 PING 命令 ；

（2）如果一个实例（instance）距离最后一次有效回复 PING 命令的时间超过 down-after-milliseconds 选项所指定的值， 则这个实例会被 Sentinel 标记为主观下线；

（3）如果一个Master被标记为主观下线，则正在监视这个Master的所有 Sentinel 要以每秒一次的频率确认Master的确进入了主观下线状态；

（4）当有足够数量的 Sentinel（大于等于配置文件指定的值）在指定的时间范围内确认Master的确进入了主观下线状态， 则Master会被标记为客观下线 ；

（5）在一般情况下， 每个 Sentinel 会以每 10 秒一次的频率向它已知的所有Master，Slave发送 INFO 命令

（6）当Master被 Sentinel 标记为客观下线时，Sentinel 向下线的 Master 的所有 Slave 发送 INFO 命令的频率会从 10 秒一次改为每秒一次 ；

（7）若没有足够数量的 Sentinel 同意 Master 已经下线， Master 的客观下线状态就会被移除；

若 Master 重新向 Sentinel 的 PING 命令返回有效回复， Master 的主观下线状态就会被移除；

## 11.13 悲观锁

执行操作前假设当前的操作肯定（或有很大几率）会被打断（悲观）。基于这个假设，我们在做操作前就会把相关资源锁定，不允许自己执行期间有其他操作干扰。

Redis不支持悲观锁。Redis作为缓存服务器使用时，以读操作为主，很少写操作，相应的操作被打断的几率较少。不采用悲观锁是为了防止降低性能。

## 11.14 乐观锁

执行操作前假设当前操作不会被打断（乐观）。基于这个假设，我们在做操作前不会锁定资源，万一发生了其他操作的干扰，那么本次操作将被放弃。

## 11.15 持久化

**（1）RDB持久化：**

每隔一段时间，将内存中的数据集写到磁盘

Redis会单独创建（fork）一个子进程来进行持久化，会先将数据写入到个临时文件中，待持久化过程都结束了，再用这个临时文件替换上次持久化好的文件。整个过程中，主进程是不进行任何IO操作的，这就确保了极高的性能如果需要进行大规模数据的恢复，且对于数据恢复的完整性不是非常敏感，那RDB方式要比AOF方式更加的高效。

**保存策略：**

save 9  00 1  900 秒内如果至少有 1 个 key 的值变化，则保存

save 300  10  300 秒内如果至少有 10 个 key 的值变化，则保存

save 60 1 0000 60 秒内如果至10000 个 key 的值变化，则保存

**（2）AOF 持久化: 以日志形式记录每个更新（(总结、改）操作**

Redis重新启动时读取这个文件，重新执行新建、修改数据的命令恢复数据。

**保存策略：**

appendfsync always：每次产生一条新的修改数据的命令都执行保存操作；效率低，但是安全！

appendfsync everysec：每秒执行一次保存操作。如果在未保存当前秒内操作时发生了断电，仍然会导致一部分数据丢失（即1秒钟的数据）。

appendfsync no：将数据库保存操作的触发时机交给操作系统来进行调度更快，也更不安全的选择。

推荐（并且也是默认）的措施为每秒 fsync 一次， 这种 fsync 策略可以兼顾速度和安全性。

**缺点：**

1 比起RDB占用更多的磁盘空间

2 恢复备份速度要慢

3 每次读写都同步的话，有一定的性能压力

4 存在个别Bug，造成恢复不能

**（3）选择策略：**

可读的日志文本，通过操作AOF

官方推荐：

如果对数据不敏感，可以选单独用RDB；不建议单独用AOF，因为可能出现Bug;如果只是做纯内存缓存，可以都不用

## 11.16 Redis提供了哪几种持久化方式？

RDB持久化方式能够在指定的时间间隔能对你的数据进行快照存储。

AOF持久化方式记录每次对服务器写的操作,当服务器重启的时候会重新执行这些命令来恢复原始的数据，AOF命令以redis协议追加保存每次写的操作到文件末尾.Redis还能对AOF文件进行后台重写,使得AOF文件的体积不至于过大。

如果你只希望你的数据在服务器运行的时候存在，你也可以不使用任何持久化方式。

你也可以同时开启两种持久化方式，在这种情况下，当redis重启的时候会优先载入AOF文件来恢复原始的数据,因为在通常情况下AOF文件保存的数据集要比RDB文件保存的数据集要完整。

## 11.17 如何选择合适的持久化方式？

一般来说， 如果想达到足以媲美PostgreSQL的数据安全性， 你应该同时使用两种持久化功能。如果你非常关心你的数据， 但仍然可以承受数分钟以内的数据丢失，那么你可以只使用RDB持久化。

有很多用户都只使用AOF持久化，但并不推荐这种方式：因为定时生成RDB快照（snapshot）非常便于进行数据库备份， 并且 RDB 恢复数据集的速度也要比AOF恢复的速度要快，除此之外， 使用RDB还可以避免之前提到的AOF程序的bug。

## 11.18 分布式Redis是前期做还是后期规模上来了再做好？为什么？

既然Redis是如此的轻量（单实例只使用1M内存）,为防止以后的扩容，最好的办法就是一开始就启动较多实例。即便你只有一台服务器，你也可以一开始就让Redis以分布式的方式运行，使用分区，在同一台服务器上启动多个实例。

一开始就多设置几个Redis实例，例如32或者64个实例，对大多数用户来说这操作起来可能比较麻烦，但是从长久来看做这点牺牲是值得的。

这样的话，当你的数据不断增长，需要更多的Redis服务器时，你需要做的就是仅仅将Redis实例从一台服务迁移到另外一台服务器而已（而不用考虑重新分区的问题）。一旦你添加了另一台服务器，你需要将你一半的Redis实例从第一台机器迁移到第二台机器。

## 11.19 Redis的内存占用情况怎么样？

给你举个例子： 100万个键值对（键是0到999999值是字符串“hello world”）在我的32位的Mac笔记本上 用了100MB。同样的数据放到一个key里只需要16MB， 这是因为键值有一个很大的开销。 在Memcached上执行也是类似的结果，但是相对Redis的开销要小一点点，因为Redis会记录类型信息引用计数等等。

当然，大键值对时两者的比例要好很多。

64位的系统比32位的需要更多的内存开销，尤其是键值对都较小时，这是因为64位的系统里指针占用了8个字节。 但是，当然，64位系统支持更大的内存，所以为了运行大型的Redis服务器或多或少的需要使用64位的系统。

## 11.20 都有哪些办法可以降低Redis的内存使用情况呢？

如果你使用的是32位的Redis实例，可以好好利用Hash,list,sorted set,set等集合类型数据，因为通常情况下很多小的Key-Value可以用更紧凑的方式存放到一起。

## 11.21 查看Redis使用情况及状态信息用什么命令？

info

## 11.22 Redis的内存用完了会发生什么？

如果达到设置的上限，Redis的写命令会返回错误信息（但是读命令还可以正常返回。）或者你可以将Redis当缓存来使用配置淘汰机制，当Redis达到内存上限时会冲刷掉旧的内容。

## 11.23 redis是单线程的，为什么那么快

1)完全基于内存，绝大部分请求是纯粹的内存操作，非常快速。数据存在内存中，类似于HashMap，HashMap的优势就是查找和操作的时间复杂度都是O(1)

2)数据结构简单，对数据操作也简单，Redis中的数据结构是专门进行设计的

3)采用单线程，避免了不必要的上下文切换和竞争条件，也不存在多进程或者多线程导致的切换而消耗 CPU，不用去考虑各种锁的问题，不存在加锁释放锁操作，没有因为可能出现死锁而导致的性能消耗

4)使用多路I/O复用模型，非阻塞IO

5)使用底层模型不同，它们之间底层实现方式以及与客户端之间通信的应用协议不一样，Redis直接自己构建了VM 机制 ，因为一般的系统调用系统函数的话，会浪费一定的时间去移动和请求

## 11.24 Redis是单线程的，如何提高多核CPU的利用率？

可以在同一个服务器部署多个Redis的实例，并把他们当作不同的服务器来使用，在某些时候，无论如何一个服务器是不够的， 所以，如果你想使用多个CPU，你可以考虑一下分片（shard）。

## 11.25 一个Redis实例最多能存放多少的keys？List、Set、Sorted Set他们最多能存放多少元素？

理论上Redis可以处理多达

![img](http://www.atguigu.com/wp-content/uploads/image-1.png)

的keys，并且在实际中进行了测试，每个实例至少存放了2亿5千万的keys。我们正在测试一些较大的值。

任何list、set、和sorted set都可以放

![img](http://www.atguigu.com/wp-content/uploads/image-2.png)

个元素。

换句话说，Redis的存储极限是系统中的可用内存值。

## 11.26 Redis常见性能问题和解决方案？

(1) Master最好不要做任何持久化工作，如RDB内存快照和AOF日志文件

(2) 如果数据比较重要，某个Slave开启AOF备份数据，策略设置为每秒同步一次

(3) 为了主从复制的速度和连接的稳定性，Master和Slave最好在同一个局域网内

(4) 尽量避免在压力很大的主库上增加从库

(5) 主从复制不要用图状结构，用单向链表结构更为稳定，即：Master <- Slave1 <- Slave2 <- Slave3…

这样的结构方便解决单点故障问题，实现Slave对Master的替换。如果Master挂了，可以立刻启用Slave1做Master，其他不变。

## 11.27 Redis相比memcached有哪些优势？

(1) memcached所有的值均是简单的字符串，redis作为其替代者，支持更为丰富的数据类型

(2) redis的速度比memcached快很多

- redis可以持久化其数据

## 11.28 MySQL里有2000w数据，redis中只存20w的数据，如何保证redis中的数据都是热点数据？

redis内存数据集大小上升到一定大小的时候，就会施行数据淘汰策略。

## 11.29 Redis有哪几种数据淘汰策略？

noeviction:返回错误当内存限制达到并且客户端尝试执行会让更多内存被使用的命令（大部分的写入指令，但DEL和几个例外）

allkeys-lru: 尝试回收最少使用的键（LRU），使得新添加的数据有空间存放。

volatile-lru: 尝试回收最少使用的键（LRU），但仅限于在过期集合的键,使得新添加的数据有空间存放。

allkeys-random: 回收随机的键使得新添加的数据有空间存放。

volatile-random: 回收随机的键使得新添加的数据有空间存放，但仅限于在过期集合的键。

volatile-ttl: 回收在过期集合的键，并且优先回收存活时间（TTL）较短的键,使得新添加的数据有空间存放。

## 11.30 Redis集群方案应该怎么做？都有哪些方案？

（1）twemproxy，大概概念是，它类似于一个代理方式，使用方法和普通redis无任何区别，设置好它下属的多个redis实例后，使用时在本地需要连接redis的地方改为连接twemproxy，它会以一个代理的身份接收请求并使用一致性hash算法，将请求转接到具体redis，将结果再返回twemproxy。使用方式简便(相对redis只需修改连接端口)，对旧项目扩展的首选。 问题：twemproxy自身单端口实例的压力，使用一致性hash后，对redis节点数量改变时候的计算值的改变，数据无法自动移动到新的节点。

（2）codis，目前用的最多的集群方案，基本和twemproxy一致的效果，但它支持在 节点数量改变情况下，旧节点数据可恢复到新hash节点。

（3）redis cluster3.0自带的集群，特点在于他的分布式算法不是一致性hash，而是hash槽的概念，以及自身支持节点设置从节点。具体看官方文档介绍。

（4）在业务代码层实现，起几个毫无关联的redis实例，在代码层，对key 进行hash计算，然后去对应的redis实例操作数据。 这种方式对hash层代码要求比较高，考虑部分包括，节点失效后的替代算法方案，数据震荡后的自动脚本恢复，实例的监控，等等。

## 11.31 说说Redis哈希槽的概念？

Redis集群没有使用一致性hash,而是引入了哈希槽的概念，Redis集群有16384个哈希槽，每个key通过CRC16校验后对16384取模来决定放置哪个槽，集群的每个节点负责一部分hash槽。

## 11.32 Redis集群最大节点个数是多少？

16384个。

## 11.33 怎么测试Redis的连通性？

ping

## 11.34 修改配置不重启Redis会实时生效吗？

针对运行实例，有许多配置选项可以通过 CONFIG SET 命令进行修改，而无需执行任何形式的重启。 从 Redis 2.2 开始，可以从 AOF 切换到 RDB 的快照持久性或其他方式而不需要重启 Redis。检索 ‘CONFIG GET *’ 命令获取更多信息。

但偶尔重新启动是必须的，如为升级 Redis 程序到新的版本，或者当你需要修改某些目前 CONFIG 命令还不支持的配置参数的时候。

## 11.35 Redis有哪些适合的场景？

（1）会话缓存（Session Cache）

最常用的一种使用Redis的情景是会话缓存（session cache）。用Redis缓存会话比其他存储（如Memcached）的优势在于：Redis提供持久化。当维护一个不是严格要求一致性的缓存时，如果用户的购物车信息全部丢失，大部分人都会不高兴的，现在，他们还会这样吗？

幸运的是，随着 Redis 这些年的改进，很容易找到怎么恰当的使用Redis来缓存会话的文档。甚至广为人知的商业平台Magento也提供Redis的插件。

（2）全页缓存（FPC）

除基本的会话token之外，Redis还提供很简便的FPC平台。回到一致性问题，即使重启了Redis实例，因为有磁盘的持久化，用户也不会看到页面加载速度的下降，这是一个极大改进，类似PHP本地FPC。

再次以Magento为例，Magento提供一个插件来使用Redis作为全页缓存后端。

此外，对WordPress的用户来说，Pantheon有一个非常好的插件 wp-redis，这个插件能帮助你以最快速度加载你曾浏览过的页面。

（3）队列

Reids在内存存储引擎领域的一大优点是提供 list 和 set 操作，这使得Redis能作为一个很好的消息队列平台来使用。Redis作为队列使用的操作，就类似于本地程序语言（如Python）对 list 的 push/pop 操作。

如果你快速的在Google中搜索“Redis queues”，你马上就能找到大量的开源项目，这些项目的目的就是利用Redis创建非常好的后端工具，以满足各种队列需求。例如，Celery有一个后台就是使用Redis作为broker，你可以从这里去查看。

（4）排行榜/计数器

Redis在内存中对数字进行递增或递减的操作实现的非常好。集合（Set）和有序集合（Sorted Set）也使得我们在执行这些操作的时候变的非常简单，Redis只是正好提供了这两种数据结构。所以，我们要从排序集合中获取到排名最靠前的10个用户–我们称之为“user_scores”，我们只需要像下面一样执行即可：

当然，这是假定你是根据你用户的分数做递增的排序。如果你想返回用户及用户的分数，你需要这样执行：

ZRANGE user_scores 0 10 WITHSCORES

Agora Games就是一个很好的例子，用Ruby实现的，它的排行榜就是使用Redis来存储数据的，你可以在这里看到。

（5）发布/订阅

最后（但肯定不是最不重要的）是Redis的发布/订阅功能。发布/订阅的使用场景确实非常多。我已看见人们在社交网络连接中使用，还可作为基于发布/订阅的脚本触发器，甚至用Redis的发布/订阅功能来建立聊天系统！（不，这是真的，你可以去核实）。

## 12. MQ

## 12.1 ActiveMQ 如果消息发送失败怎么办？

Activemq 有两种通信方式，点到点形式和发布订阅模式。

如果是点到点模式的话，如果消息发送不成功此 消息默认会保存到 activemq 服务端直到有消费者将其消费，所以此时消息是不会丢失的。

如果是发布订阅模式的通信方式，默认情况下只通知一次，如果接收不到此消息就没有了。这种场景只适 用于对消息送达率要求不高的情况。如果要求消息必须送达不可以丢失的话，需要配置持久订阅。每个订阅端定义一个 id， 在订阅是向 activemq 注册。发布消息和接收消息时需要配置发送模式为持久化。此时 如果客户端接收不到消息，消息会持久化到服务端，直到客户端正常接收后为止。

## 12.2 如何使用ActiveMQ 解决分布式事务？

在互联网应用中，基本都会有用户注册的功能。在注册的同时，我们会做出如下操作：

收集用户录入信息，保存到数据库向用户的手机或邮箱发送验证码等等…

如果是传统的集中式架构，实现这个功能非常简单：开启一个本地事务，往本地数据库中插入一条用户数据，发送验证码，提交事务。

但是在分布式架构中，用户和发送验证码是两个独立的服务，它们都有各自的数据库，那么就不能通过本地事务保证操作的原子性。这时我们就需要用到 ActiveMQ（消息队列）来为我们实现这个需求。

在用户进行注册操作的时候，我们为该操作创建一条消息，当用户信息保存成功时，把这条消息发送到消息队列。验证码系统会监听消息，一旦接受到消息，就会给该用户发送验证码。

## 12.3 如何防止ActiveMQ消息重复发送？

解决方法很简单：增加消息状态表。通俗来说就是一个账本，用来记录消息的处理状态，每次处理消息之前，都去状态表中查询一次，如果已经有相同的消息存在，那么不处理，可以防止重复发送。

## 13. ElasticSearch

## 13.1 什么是ElasticSearch？ 

Elasticsearch是一个基于Lucene的搜索引擎。它提供了具有HTTP Web界面和无架构JSON文档的分布式，多租户能力的全文搜索引擎。Elasticsearch是用Java开发的，根据Apache许可条款作为开源发布。

## 13.2 Elasticsearch中的倒排索引是什么？ 

倒排索引是搜索引擎的核心。搜索引擎的主要目标是在查找发生搜索条件的文档时提供快速搜索。倒排索引是一种像数据结构一样的散列图，可将用户从单词导向文档或网页。它是搜索引擎的核心。其主要目标是快速搜索从数百万文件中查找数据。 

## 14. Dubbo

## 14.1 Dubbo 的连接方式有哪些？

Dubbo 的客户端和服务端有三种连接方式，分别是：广播，直连和使用 zookeeper 注册中心。

## 14.2 Dubbo 的容错机制有哪些？

（1）Failover Cluster 模 式

失败自动切换，当出现失败，重试其它服务器。(默认) 2）Failfast Cluster

快速失败，只发起一次调用，失败立即报错。 通常用于非幂等性的写操作，比如新增记录。

（2）Failsafe Cluster

失败安全，出现异常时，直接忽略。 通常用于写入审计日志等操作。

（3）Failback Cluster

失败自动恢复，后台记录失败请求，定时重发。 通常用于消息通知操作。

（4）Forking Cluster

并行调用多个服务器，只要一个成功即返回。通常用于实时性要求较高的读操作，但需要浪费更多服务资源。可通过 forks=”2”来设置最大并行数。

（5）Broadcast Cluster

广播调用所有提供者，逐个调用，任意一台报错则报错。(2.1.0 开始支持) 通常用于通知所有提供者更新缓存或日志等本地资源信息。

总结： 在实际应用中查询语句容错策略建议使用默认Failover Cluster ，而增删改建议使用 Failfast Cluster 或者 使用 Failover Cluster（retries=”0”） 策略 防止出现数据 重复添加等等其它问题！建议在设计接口时候把查询接口方法单独做一个接口提供查询。

## 14.3 使用dubbo 遇到过哪些问题？

（1）增加提供服务版本号和消费服务版本号

这个具体来说不算是一个问题,而是一种问题的解决方案,在我们的实际工作中会面临各种环境资源短缺的问题,也是很实际的问题,刚开始我们还可以提供一个服务进行相关的开发和测试,但是当有多个环境多个版本,多个任务的时候就不满足我们的需求,这时候我们可以通过给提供方增加版本的方式来区分.这样能够剩下很多的物理资源,同时为今后更换接口定义发布在线时，可不停机发布，使用版本号.

引用只会找相应版本的服务,例如：

<dubbo:serviceinterface=“com.xxx.XxxService”ref=“xxxService” version=“1.0” />

<dubbo:referenceid=“xxxService”interface=“com.xxx.XxxService” version=“1.0”/>

（2）dubbo reference 注解问题

@Reference 只能在 springbean 实例对应的当前类中使用，暂时无法在父类使用；如果确实要在父类声明一个引用，可通过配置文件配置 dubbo:reference，然后在需要引用的地方跟引用 springbean 一样就可以了.

（3）出现 RpcException: No provider available for remote service 异常，表示没有可用的服务提供者

- 检查连接的注册中心是否正确
- 到注册中心查看相应的服务提供者是否存在
- 检查服务提供者是否正常运行

（4）服务提供者没挂，但在注册中心里看不到

首先，确认服务提供者是否连接了正确的注册中心，不只是检查配置中的注册中心地址，而且要检查实际的网络连接。

其次，看服务提供者是否非常繁忙，比如压力测试，以至于没有CPU 片段向注册中心发送心跳，这种情况，减小压力，将自动恢复。

## 15. Zookeeper

## 15.1 ZooKeeper是什么？

ZooKeeper是一个开放源码的分布式协调服务，它是集群的管理者，监视着集群中各个节点的状态根据节点提交的反馈进行下一步合理操作。最终，将简单易用的接口和性能高效、功能稳定的系统提供给用户。

分布式应用程序可以基于Zookeeper实现诸如数据发布/订阅、负载均衡、命名服务、分布式协调/通知、集群管理、Master选举、分布式锁和分布式队列等功能。

Zookeeper保证了如下分布式一致性特性：

- 顺序一致性
- 原子性
- 单一视图
- 可靠性
- 实时性（最终一致性）

客户端的读请求可以被集群中的任意一台机器处理，如果读请求在节点上注册了监听器，这个监听器也是由所连接的zookeeper机器来处理。对于写请求，这些请求会同时发给其他zookeeper机器并且达成一致后，请求才会返回成功。因此，随着zookeeper的集群机器增多，读请求的吞吐会提高但是写请求的吞吐会下降。

有序性是zookeeper中非常重要的一个特性，所有的更新都是全局有序的，每个更新都有一个唯一的时间戳，这个时间戳称为zxid（Zookeeper Transaction Id）。而读请求只会相对于更新有序，也就是读请求的返回结果中会带有这个zookeeper最新的zxid。

## 15.2 Zookeeper Watcher 机制 — 数据变更通知

Zookeeper允许客户端向服务端的某个Znode注册一个Watcher监听，当服务端的一些指定事件触发了这个Watcher，服务端会向指定客户端发送一个事件通知来实现分布式的通知功能，然后客户端根据Watcher通知状态和事件类型做出业务上的改变。

**工作机制：**

- 客户端注册watcher
- 服务端处理watcher
- 客户端回调watcher

**Watcher   特性总结：**

（1）一次性
无论是服务端还是客户端，一旦一个Watcher被触发，Zookeeper都会将其从相应的存储中移除。这样的设计有效的减轻了服务端的压力，不然对于更新非常频繁的节点，服务端会不断的向客户端发送事件通知，无论对于网络还是服务端的压力都非常大。

（2）客户端串行执行
客户端Watcher回调的过程是一个串行同步的过程。

（3）轻量

Watcher通知非常简单，只会告诉客户端发生了事件，而不会说明事件的具体内容。

客户端向服务端注册Watcher的时候，并不会把客户端真实的Watcher对象实体传递到服务端，仅仅是在客户端请求中使用boolean类型属性进行了标记。

watcher event异步发送watcher的通知事件从server发送到client是异步的，这就存在一个问题，不同的客户端和服务器之间通过socket进行通信，由于网络延迟或其他因素导致客户端在不同的时刻监听到事件，由于Zookeeper本身提供了ordering guarantee，即客户端监听事件后，才会感知它所监视znode发生了变化。所以我们使用Zookeeper不能期望能够监控到节点每次的变化。Zookeeper只能保证最终的一致性，而无法保证强一致性。

注册watcher getData、exists、getChildren

触发watcher create、delete、setData

当一个客户端连接到一个新的服务器上时，watch将会被以任意会话事件触发。当与一个服务器失去连接的时候，是无法接收到watch的。而当client重新连接时，如果需要的话，所有先前注册过的watch，都会被重新注册。通常这是完全透明的。只有在一个特殊情况下，watch可能会丢失：对于一个未创建的znode的exist watch，如果在客户端断开连接期间被创建了，并且随后在客户端连接上之前又删除了，这种情况下，这个watch事件可能会被丢失。

## 16. Git

## 16.1 reset 与 rebase, pull 与 fetch 的区别

git reset 不修改commit相关的东西，只会去修改.git目录下的东西。

git rebase 会试图修改你已经commit的东西，比如覆盖commit的历史等，但是不能使用rebase来修改已经push过的内容，容易出现兼容性问题。rebase还可以来解决内容的冲突，解决两个人修改了同一份内容，然后失败的问题。

git pull pull=fetch+merge,

使用git fetch是取回远端更新，不会对本地执行merge操作，不会去动你的本地的内容。                                                      pull会更新你本地代码到服务器上对应分支的最新版本

## 16.2 git merge和git rebase的区别

git merge把本地代码和已经取得的远程仓库代码合并。

git rebase是复位基底的意思，gitmerge会生成一个新的节点，之前的提交会分开显示，而rebase操作不会生成新的操作，将两个分支融合成一个线性的提交。

## 16.3 git如何解决代码冲突

git stash

git pull

git stash pop

这个操作就是把自己修改的代码隐藏，然后把远程仓库的代码拉下来，然后把自己隐藏的修改的代码释放出来，让git自动合并。

如果要代码库的文件完全覆盖本地版本。

git reset –hard

git pull

## 17. Linux

## 17.1 Linux常用命令

| 序号 | 命令                          | 命令解释                               |
| ---- | ----------------------------- | -------------------------------------- |
| 1    | top                           | 查看内存                               |
| 2    | df -h                         | 查看磁盘存储情况                       |
| 3    | iotop                         | 查看磁盘IO读写(yum install iotop安装） |
| 4    | iotop -o                      | 直接查看比较高的磁盘读写程序           |
| 5    | netstat -tunlp \| grep 端口号 | 查看端口占用情况                       |
| 6    | uptime                        | 查看报告系统运行时长及平均负载         |
| 7    | ps aux                        | 查看进程                               |

## 17.2 如何查看所有java进程

grep是搜索关键字

\>ps -ef | grep java

-aux 显示所有状态

\>ps -aux | grep java

## 17.3 如何杀掉某个服务的进程

kill 命令用于终止进程

-9 强迫进程立即停止

\>kill -9 [PID]

这里pid需要用 ps -ef | grep 查询pid

![IMG_256](http://www.atguigu.com/wp-content/uploads/image035.png)

## 17.4 启动/停止服务

以启动Tomcat为例,先cd到启动的.sh文件目录

\> cd /java/tomcat/bin

\> ./startup.sh

停止Tomcat服务命令

\>./shutdown.sh

## 17.5 如何查看测试项目的日志

一般测试的项目里面，有个logs的目录文件，会存放日志文件，有个xxx.out的文件，可以用tail -f 动态实时查看后端日志

先cd 到logs目录(里面有xx.out文件)

\>tail -f xx.out

这时屏幕上会动态实时显示当前的日志，ctr+c停止

## 17.6 如何查看最近1000行日志

\>tail -1000 xx.out

## 17.7 LINUX中如何查看某个端口是否被占用

\>netstat -anp | grep 端口号

![IMG_256](http://www.atguigu.com/wp-content/uploads/image037.png)

图中主要看监控状态为LISTEN表示已经被占用，最后一列显示被服务mysqld占用，查看具体端口号，只要有如图这一行就表示被占用了

查看82端口的使用情况，如图

\>netstat -anp |grep 82

![IMG_256](http://www.atguigu.com/wp-content/uploads/image039.png)

可以看出并没有LISTEN那一行，所以就表示没有被占用。此处注意，图中显示的LISTENING并不表示端口被占用，不要和LISTEN混淆哦，查看具体端口时候，必须要看到tcp，端口号，LISTEN那一行，才表示端口被占用了

## 17.8 查看当前所有已经使用的端口情况

如图：

netstat -nultp（此处不用加端口号）

![IMG_256](http://www.atguigu.com/wp-content/uploads/image041.png)

## 17.9 如何查找一个文件大小超过5M的文件

\>find . -type f -size +100M

## 17.10 如果知道一个文件名称，怎么查这个文件在linux下的哪个目录

如：要查找tnsnames.ora文件

\>find / -name tnsnames.ora

查到：

/opt/app/oracle/product/10.2/network/admin/tnsnames.ora

/opt/app/oracle/product/10.2/network/admin/samples/tnsnames.ora

还可以用locate 来查找

\>locate tnsnames.ora

结果是：

/opt/app/oracle/product/10.2/hs/admin/tnsnames.ora.sample

/opt/app/oracle/product/10.2/network/admin/tnsnames.ora

/opt/app/oracle/product/10.2/network/admin/samples/tnsnames.ora

## 17.11 find查找文件

find / -name httpd.conf　　#在根目录下查找文件httpd.conf，表示在整个硬盘查找

find /etc -name httpd.conf　　#在/etc目录下文件httpd.conf

find /etc -name ‘srm’　　#使用通配符(0或者任意多个)。表示在/etc目录下查找文件名中含有字符串‘srm’的文件

find . -name ‘srm’ 　　#表示当前目录下查找文件名开头是字符串‘srm’的文件

按照文件特征查找 　　　　

find / -amin -10 　　# 查找在系统中最后10分钟访问的文件(access time)

find / -atime -2　　 # 查找在系统中最后48小时访问的文件

find / -empty 　　# 查找在系统中为空的文件或者文件夹

find / -group cat 　　# 查找在系统中属于 group为cat的文件

find / -mmin -5 　　# 查找在系统中最后5分钟里修改过的文件(modify time)

find / -mtime -1 　　#查找在系统中最后24小时里修改过的文件

find / -user fred 　　#查找在系统中属于fred这个用户的文件

find / -size +10000c　　#查找出大于10000000字节的文件(c:字节，w:双字，k:KB，M:MB，G:GB)

find / -size -1000k 　　#查找出小于1000KB的文件

## 17.12 vim（vi）编辑器

有命令模式、输入模式、末行模式三种模式。

- ● 命令模式：查找内容(/abc、跳转到指定行(20gg)、跳转到尾行(G)、跳转到首行(gg)、删除行(dd)、插入行(o)、复制粘贴(yy,p)
- ● 输入模式：编辑文件内容
- ● 末行模式：保存退出(wq)、强制退出(q!)、显示文件行号(set nu)

在命令模式下，输入a或i即可切换到输入模式，输入冒号(:)即可切换到末行模式；在输入模式和末行模式下，按esc键切换到命令模式
# Java笔记

## 1.Class `ThreadLocalRandom`

![image-20210309142235122](C:\Users\14283\AppData\Roaming\Typora\typora-user-images\image-20210309142235122.png)

利用`current()`返回一个`ThreadLocalRandom`类的实体，通过这个实体，调用类中所有的函数，所以`ThreadLocalRandom`类的用法为`ThreadLocalRandom.current().nextX(...)`X是`Int,Long`等等

## 2.Class `SimpleDateFormat`

```java
package com.Google;

import java.text.DateFormat;
import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.Date;

public class Test{
    public static void main(String args[]) throws ParseException {
        DateFormat dateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
        String nowTime = "2021-03-09 19:45:03";
        Date date = dateFormat.parse(nowTime);
        System.out.println(date);
    }
}
```

向上转型——父类new子类

向下转型——子类 = (父类) 父类实例 （强制转换）

## 3.Junit

## 4.String

### StringBuilder

### StringBuffer

## 5.Throwable

### Error

### Exception

`Exception` 编译时报错

`RunTimeException` 运行时报错

### 抛出异常与捕获异常

捕获异常是指发生异常时，做相应处理，避免程序崩溃
try catch对抛出或可能抛出的进行捕获并对捕获到的异常进行处理

抛出异常是让程序知道哪里可能会存在异常，发生异常后，回滚处理

**小总结**
抛出异常：
创建异常对象，封装异常信息然后通过throw将异常对象传递给调用者。
不对异常进行处理只对异常进行抛出是非常不负责任的表现可以称为渣男。
但是可以通过主动抛出异常对一些jvm虚拟机识别不出来的异常进行抛出。
手动抛出异常举例

```java
public static void main(String[] args) throws Exception {
        int age = 0;
        age = -100;
        if(age<0)
        {
            Exception e = new Exception();//创建异常对象
            throw e;//抛出异常
        }
        System.out.println(age);
    }
```

这个例子在常理中年龄是不能小于零的所以要手动抛出异常。
捕获异常：
对异常进行捕获然后进行指定方式的处理

throw与throws的区别：
1.抛出的东西不同：throw抛出的是具体的异常对象，而throws抛出的是抽象的异常类。
2.使用位置不同：throw一般用在方法体中，也可用在代码块中，throws只能用在方法声明括号后面。

## 7.继承与多态

* 子类实例化对象时，会先调用父类的构造器
* 如果子类的构造器没有显示的调用父类的构造器 ，默认调用super();
* 子类要使用父类有参的构造器，使用super（参数）形式，且super必须是子类构造方法中的头一条语句。
* 如果父类没有不带参数的构造器，且子类的构造器中又没显示的调用父类其他构造器，则Java编译器将报告错误。
* 对于调用父类成员变量还是子类成员变量，只与变量的声明类型有关系，与实例化的类型没有关系。而对于调用父类方法还是子类方法，只与变量的实例化的类型有关系，与声明的类型没有关系，当然是在方法被重写的情况下，如果没有重写，则调用的是父类的方法。

## 8.final

1. 修饰类：此类不能被继承
2. 修饰方法：此类不能被重写，但可以被子类使用（public）
3. 修饰变量：此变量永远不能再改变。

## 9.abstract (抽象类和抽象方法)

Animal本质来说是没人用的，它是一个抽象的，它抽取了猫和狗这些东西的共性做为使用

抽象------具体

动物------狗、猫

抽象的目的是为了概括（解释）这些具体事物

1. 修饰类：抽象类不能实例化，抽象类是对具体事务的抽象
2. 修饰方法：抽象方法：抽象方法不能拥有函数体，父类的抽象方法子类必须重写实现。换言之，当一个类继承一个抽象类时，该子类必须重写父类中所有的抽象方法。
3. 抽象类中可以没有抽象方法；抽象方法出现在类中，则该类必须是抽象的。

## 10.super

java中的`super`关键字是一个引用变量，用于引用直接父类对象。

每当创建子类的实例时，父类的实例被隐式创建，由`super`关键字引用变量引用。

java `super`关键字的用法如下：

- `super`可以用来引用直接父类的实例变量。
- `super`可以用来调用直接父类方法。
- `super()`可以用于调用直接父类构造函数。

## 11.interface

抽象类是对具体事务的抽象，接口是对行为(动作)进行抽象。

接口的设计目的，是对类的行为进行约束（更准确的说是一种“有”约束，因为接口不能规定类不可以有什么行为），也就是提供一种机制，可以强制要求不同的类具有相同的行为。它只约束了行为的有无，但不对如何实现行为进行限制。

## 12.Object

超类，所有类的父类。

实例程序：`toString()`函数是典型的Object类的函数，所以任何类中的`toString()`函数都是被重写的，会有`@Override`注解（该注解会告诉编译器检查这个方法，保证父类要含有一个被重写的方法，否则就会编译出错）

```java
@Override
public String toString() {
    return "MyThread{" +
            "i=" + i +
            '}';
}
```

## 13.多线程

### 后台守护线程：`thread.setDaemon(true)`

线程非安全不同步：new一个锁对象处理

### 同步方法：

用 **synchronized** 关键字给针对共享资源进行操作的方法加锁。一个方法使用 **synchronized** 关键字修饰后，当一个线程A使用这个方法时，其他线程想使用这个方法时就必须等待，直到线程A使用完该方法。

```java
package com.Microsoft;

public class FrankThread implements Runnable {
    private int shoesCount = 10;

    // 锁对象
    Object lock = new Object();

    @Override
    public void run() {
        while (true) {
            nikeCatch();
        }
    }

    // 同步方法
    public synchronized void nikeCatch() {
        // 同步代码块
        if (shoesCount > 0) {
            // 线程非安全不同步
            try {
                Thread.sleep(500);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(Thread.currentThread().getName() + "抢到第" + (shoesCount--) + "双鞋");
        }
    }
}
```

### 同步代码块：

利用 **同步块** ，也就是用 **synchronized** 关键字来修饰的代码块来解决问题，需要给对象加锁。每一个对象都有一个 **监视器** 或者叫 **锁** 。

```java
package com.Microsoft;

public class NikolaThread implements Runnable {
    private int shoesCount = 10;

    // 锁对象
    Object lock = new Object();

    @Override
    public void run() {
        while (true) {
            // 同步代码块
            synchronized(lock){
                if (shoesCount > 0) {
                    // 线程非安全不同步
                    try {
                        Thread.sleep(500);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    System.out.println(Thread.currentThread().getName() + "抢到第" + (shoesCount--) + "双nike鞋");
                }
            }
        }
    }
}

```

### ReentrantLock

Java自带同步锁 Lock接口，可以new它的实践类ReentrantLock

- java中已经有了内置锁：`synchronized`,`synchronized`的特点是使用简单，一切交给JVM去处理,不需要显示释放
- 从用法上可以看出，与`synchronized`相比， `ReentrantLock`就稍微复杂一点。因为必须在finally中进行解锁操作，如果不在 finally解锁，有可能代码出现异常锁没被释放，

> 那么为什么要引入ReentrantLock呢？

- 在jdk1.5里面，`ReentrantLock`的性能是明显优于`synchronized`的，但是在jdk1.6里面，`synchronized`做了优化，他们之间的性能差别已经不明显了。

![img](https:////upload-images.jianshu.io/upload_images/4360245-91de4add7ec21b4d.png?imageMogr2/auto-orient/strip|imageView2/2/w/1188/format/webp)

- `ReentrantLock`并不是一种替代内置加锁的方法，而是作为一种可选择的高级功能。
- 相比于`synchronized`，`ReentrantLock`在功能上更加丰富，它具有***可重入、可中断、可限时、公平锁\***等特点。

> ReentrantLock  实现了 [Lock interface](https://link.jianshu.com?t=http://docs.oracle.com/javase/1.5.0/docs/api/java/util/concurrent/locks/Lock.html#method_summary)

### CPU 线程调度
每一个线程的使用优先权都是系统随机分配的，谁先分配到谁先用
耍赖：赋予某个线程至高无上的的优先使用权

系统是：轮流获得
Java操作方式：抢占CPU资源

1-10 是Java优先级的等级范围
main()主线程 value=5 默认优先级NORM_PRIORITY
thread.setPriority()可以设置线程的优先级
但是由于CPU的执行速度太快了，往往导致线程执行完了，优先级调度还没执行完，程序就结束了，呈现出一种默认随机的现象。而且不同的操作系统对线程优先级调度的支持也不同。（这点在Java中尤其明显）

### Tips:

`thread.join()`线程插队

`thread.sleep(millis)`线程休眠

`thread.yield()` 线程让步

### 线程状态

共6种

#### new 新建

`new Thread(FrankThread,"thread_1");`

新建状态，当一个线程被创建分配内存时就是属于这种状态。
![在这里插入图片描述](https://img-blog.csdnimg.cn/55eac8f492f44cc1b4bd30b10de7ddca.png)

#### Runnable 可运行

`new Thread(FrankThread, "thread_1").start()`

运行状态，当线程执行start()方法时，线程就处于此状态，但是此状态不一定是线程代码在执行中。因为执行start后，线程进入等待分配CPU资源，等到分配了CPU资源后才是真正的执行线程代码。
![在这里插入图片描述](https://img-blog.csdnimg.cn/33c5524e9b0c48869a78906caa77b830.png)

#### Blocked 阻塞

阻塞状态，这个状态就是当一把锁被占有时，另外一个线程去拿锁失败，那么就进入了阻塞BLOCKED状态，这个可以是同步方法/同步代码块。被阻塞的线程在对象头有一套机制（一堆队列组成）拿锁，这里就不研究，当拿到锁时BLOCKED状态就会解除。

多个线程公用一把锁，拿到锁的进入Runnable(其中的ready)状态，等待线程调度的调度，其余的为阻塞状态。其他的线程不需要锁的start()后直接进入ready状态

#### Waiting 等待

等待状态，当线程进入阻塞后，就是WAITING状态。Thread内部枚举类State，里面有说明

![在这里插入图片描述](https://img-blog.csdnimg.cn/e4851a287f744f469ac35c1e81bb1d46.png)

文档说的很清楚，就是调用wait()、join()无参方法和park()方法可以使得线程进入WAITING状态（我自己用代码去尝试过，代码太长就不贴了）
ps：我上面说了使线程其实就是个模糊词，比如像wait方法肯定就是调用它线程，join方法却是执行此方法的线程，比如main中调用t.join()，那么main进入WAITING。

#### Time Waiting 计时等待

处于这种状态的线程不会被分配CPU执行时间，不过无须无限期等待被其他线程显示地唤醒，在达到一定时间后它们会自动唤醒。

#### Terminated 终止

终止状态，当run方法中线程代码执行完毕，那么线程就进入这种状态。

#### ps:

1. java.lang.Thread.State可以看到线程的状态
2. wait方法只能在同步方法和同步代码块中使用，否则java.lang.IllegalMonitorStateException
3. 在main函数中，wait方法是引起当前调用方法的线程阻塞，而不是调用对象线程阻塞，就是main阻塞
4. 当sleep中的线程被调用interrupt()时,就会放弃暂停的状态(TIMED_WAITING-RUNNABLE).并抛出InterruptedException.

#### 几个方法的比较

1. Thread.sleep(long millis)，一定是当前线程调用此方法，当前线程进入TIMED_WAITING状态，但不释放对象锁，millis后线程自动苏醒进入就绪状态。作用：给其它线程执行机会的最佳方式。
2. Thread.yield()，一定是当前线程调用此方法，当前线程放弃获取的CPU时间片，但不释放锁资源，由运行状态变为就绪状态，让OS再次选择线程。作用：让相同优先级的线程轮流执行，但并不保证一定会轮流执行。实际中无法保证yield()达到让步目的，因为让步的线程还有可能被线程调度程序再次选中。Thread.yield()不会导致阻塞。该方法与sleep()类似，只是不能由用户指定暂停多长时间。
3. thread.join()/thread.join(long millis)，当前线程里调用其它线程t的join方法，当前线程进入WAITING/TIMED_WAITING状态，当前线程不会释放已经持有的对象锁。线程t执行完毕或者millis时间到，当前线程一般情况下进入RUNNABLE状态，也有可能进入BLOCKED状态（因为join是基于wait实现的）。
4. obj.wait()，当前线程调用对象的wait()方法，当前线程释放对象锁，进入等待队列。依靠notify()/notifyAll()唤醒或者wait(long timeout) timeout时间到自动唤醒。
5. obj.notify()唤醒在此对象监视器上等待的单个线程，选择是任意性的。notifyAll()唤醒在此对象监视器上等待的所有线程。
6. LockSupport.park()/LockSupport.parkNanos(long nanos),LockSupport.parkUntil(long deadlines), 当前线程进入WAITING/TIMED_WAITING状态。对比wait方法,不需要获得锁就可以让线程进入WAITING/TIMED_WAITING状态，需要通过LockSupport.unpark(Thread thread)唤醒。

### 线程通信

典型例子：生产者和消费者之间以商品为信息进行通信。

生产者类：

```java
package com.Microsoft;

public class Producer extends Thread {
    private Condom condom;

    public Producer(Condom condom) {
        this.condom = condom;
    }

    @Override
    public void run() {
        while (true) {
            synchronized (condom) {
                // 是否有库存，如果有，就等。没有就生产
                if (condom.isStatus == true) {
                    try {
                        condom.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                                    }
                // 模拟商品生产完了
                condom.isStatus = true;
                System.out.println(Thread.currentThread().getName() + "我生产完了，库存有很多，消费者不要着急");
                condom.notify();    //唤醒随机一个其他的线程
            }
        }
    }
}
```

消费者类：

```java
package com.Microsoft;

public class Customer extends Thread {
    private Condom condom;

    public Customer(Condom condom) {
        this.condom = condom;
    }

    @Override
    public void run() {
        while (true) {
            synchronized (condom) {
                // 是否拥有库存？如果没有，就应该通知厂商，我们等！
                if (condom.isStatus == false) {
                    try {
                        // 没有商品了，消费者死等。
                        condom.wait();
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
                // 模拟商品卖光了，
                condom.isStatus = false;
                System.out.println(Thread.currentThread().getName() + "我买完了，你抓紧生产，我通知了哈，生产者搞快点。");
                condom.notify();    //唤醒随机一个其他的线程
            }
        }
    }
}
```

主函数：

```java
package com.Microsoft;

public class Main {

    public static void main(String[] args) throws InterruptedException {
        /**********两个线程相互通信的演示**********/

        Condom condom = new Condom();

        new Customer(condom).start();
        new Producer(condom).start();

    }
}
```

## Java Collections Framework

**java.util.Collection 下的接口和继承类关系简易结构图：**

![img](http://www.justdojava.com/assets/images/2019/java/image-jay/c25904af60394296a36c41d0c3749ab4.jpg)

**java.util.Map 下的接口和继承类关系简易结构图：**

![img](http://www.justdojava.com/assets/images/2019/java/image-jay/4c0ea9d4d39c4ab09ed7e81ac76993d1.jpg)

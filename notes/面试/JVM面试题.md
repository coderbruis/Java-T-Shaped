### 1. JVM类加载的详细过程？

### 2. JVM是如何加载Java类的？

### 3. Java类加载器包括⼏种？它们之间的⽗⼦关系是怎么样的？双亲委派机制是什么意思？有什么好处？

启动Bootstrap类加载、扩展Extension类加载、系统System类加载。

父子关系如下：

启动类加载器 ，由C++ 实现，没有父类；
扩展类加载器，由Java语言实现，父类加载器为null；
系统类加载器，由Java语言实现，父类加载器为扩展类加载器；
自定义类加载器，父类加载器肯定为AppClassLoader。
双亲委派机制：类加载器收到类加载请求，自己不加载，向上委托给父类加载，父类加载不了，再自己加载。 优势避免Java核心API篡改。

### 4. 自定义类加载器怎么实现？

【扩展】其中哪个方法走双亲委派模型，哪个不走，不走的话怎么加载类（实现findclass方法，一般用defineclass加载外部类），如何才能不走双亲委派。（重写loadclass方法）

### 5. 类加载器的双亲委派模型的作用，能重复加载某个类吗？

### 6. JVM内存模型是什么？

### 7. JVM中为什么推荐要将-Xmx和-Xms设置大小一样？

### 8. Perm Space中保存什么数据？会引起OutOfMemory吗？

加载class文件。

会引起，出现异常可以设置 -XX:PermSize 的大小。JDK 1.8后，字符串常量不存放在永久带，而是在堆内存中，JDK8以后没有永久代概念，而是用元空间替代，元空间不存在虚拟机中，二是使用本地内存。

### 9. JDK 1.8之后Perm Space有哪些变动? MetaSpace大小默认是无限的么? 还是你们会通过什么式来指定?

JDK 1.8后用元空间替代了 Perm Space；字符串常量存放到堆内存中。

MetaSpace大小默认没有限制，一般根据系统内存的大小。JVM会动态改变此值。

1. -XX:MetaspaceSize：分配给类元数据空间（以字节计）的初始大小（Oracle逻辑存储上的初始高水位，the initial high-water-mark）。此值为估计值，MetaspaceSize的值设置的过大会延长垃圾回收时间。垃圾回收过后，引起下一次垃圾回收的类元数据空间的大小可能会变大。
2. -XX:MaxMetaspaceSize：分配给类元数据空间的最大值，超过此值就会触发Full GC，此值默认没有限制，但应取决于系统内存的大小。JVM会动态地改变此值。

### 10. 了解逃逸分析算法嘛？说一下原理与作用呢？

### 11. 垃圾回收机制是什么？回收步骤有哪些？

一个对象被垃圾回收的过程：

1. 对象没有与GC Roots的引用链连接；
2. 被第一次标记为可回收状态；
3. 进行一次筛选；
4. 判断是否有必要执行finalize()方法；
5. 有必要的话，对象会被放置在F-Queue队列中；
6. 虚拟机的Finalizer线程会调用对象的finalize()方法；
7. 对象在finalize()方法里通过将this对象与类变量或者对象的成员变量进行了关联，也就与引用链上的对象进行了关联；
8. 自救成功，然后从F-Queue中被移除出去；如果被判断为没有必要执行finalize()方法；
9. 在GC对F-Queue进行第二次小规模标记的时候，被标记为可回收状态；
10. 下次垃圾回收，就会回收掉这个对象了



### 12. 项目中如何查看垃圾回收？

### 13. jvm关于gc的命令，知道多少？

### 14. 详细说一下CMS的作用，原理以及回收过程，会停顿（STW）几次？为什么会停顿？

### 15. 详细说一下G1的作用，原理以及回收过程？

### 16. 如何利用Unsafe API绕开JVM的控制？ 

### 17. 频繁YOUNGGC怎么查问题?


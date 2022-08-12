---
sidebar_position: 1
---

## 1 各自的特点

### 1.1 String

1. 在 `Java`中字符串属于对象，`Java`提供了 `String`类来**创建和操作字符串**。
2. `String`的值是**不可变**的，这就导致每次对 `String`的操作都会**生成新的 `String`对象**，这样不仅效率低下，而且大量浪费有限的内存空间，下图是对 `String`操作时内存变化的图：

   ![](https://notebook.grayson.top/media/202105//1621914583.6706944.png)

   1. 我们可以看到，初始`String`值是`hello`，然后在这个字符串后面加上新的字符串`world`，这个过程是需要在**堆内存**中开辟内存空间的，最终得到了`hello world`字符串也需要开辟相应的内存空间。
   2. 这样短短的两个字符串，却要开辟三次内存空间，这是对内存空间的极大浪费。

### 1.2 StringBuffer和StringBuilder

![StringBuffer Vs StringBuilder](https://notebook.grayson.top/media/202105//1621914583.7803657.png)

1. `StringBuffer`始于`Java 1.0`，`StringBuilder`始于`Java 1.5`。
2. `StringBuffer`的所有方法都是**同步**（Synchronized）的，因此它是**线程安全**的，这就导致相比于`StringBuilder`，它在**性能上会差一点**；`StringBuilder`的方法**不是同步的**（Non-Synchronized），因此它是**线程不安全**的，因此相比于`StringBuffer`，他在**性能上会好一点**。
3. 由于`StringBuilder`相较于`StringBuffer`有速度优势，所以大多数情况下**建议使用 `StringBuilder`类**，然而在应用程序要求**线程安全**的情况下，则**必须使用 `StringBuffer`类**。

## 2 三者的区别

1. **字符串修改**上的区别：

   1. **String：** 不可变字符串。
   2. **StringBuffer：** 可变字符串，效率低，线程安全。
   3. **StringBuilder：** 可变字符串，效率高，线程不安全。
2. **初始化**上的区别：

   1. **String：** 可以赋空值。
   2. **StringBuffer和StringBuilder：** 不能赋空值。

   ```java
   ①String
   String s = null;   
   String s = “abc”;   

   ②StringBuffer
   StringBuffer s = null; //结果警告：Null pointer access: The variable result can only be null at this location
   StringBuffer s = new StringBuffer();//StringBuffer对象是一个空的对象
   StringBuffer s = new StringBuffer(“abc”);//创建带有内容的StringBuffer对象,对象的内容就是字符串”
   ```

## 3 建议

1. 如果要操作**少量的数据**用`String`。
2. **多线程**字符串缓冲区下操作**大量数据**用`StringBuffer`。
3. **单线程**字符串缓冲区下操作**大量数据**用`StringBuilder`。

## 4 参考文献

1. [String vs StringBuffer vs StringBuilder](https://www.journaldev.com/538/string-vs-stringbuffer-vs-stringbuilder)。
2. [图析:String,StringBuffer与StringBuilder的区别](https://blog.csdn.net/weixin_41101173/article/details/79677982)。

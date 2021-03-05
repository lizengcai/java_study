# Java 

## 1-Java基础

### 1. 基础概念与常识

#### 1.1. Java 语言有哪些特点

- Java 语言特点
  - 简单易学；
  - 面向对象（封装，继承，多态）；
  - 平台无关性（ Java 虚拟机实现平台无关性）；
  - 可靠性；
  - 安全性；
  - 支持多线程；
  - 支持网络编程并且很方便（ Java 语言诞生本身就是为简化网络编程设计的，因此 Java 语言不仅支持网络编程而且很方便）；
  - 编译与解释并存

#### 1.2. 关于 JVM、JDK 和 JRE 

1、JVM

- Java 虚拟机（JVM）是运行 Java 字节码(class文件)的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果
- 什么是字节码?采用字节码的好处是什么?
  - 在 Java 中，JVM 可以理解的代码就叫做字节码（即扩展名为`.class`的文件），它不面向任何特定的处理器，只面向虚拟机。Java 语言通过字节码的方式，在一定程度上解决了传统解释型语言执行效率低的问题，同时又保留了解释型语言可移植的特点。所以 Java 程序运行时比较高效，而且，由于字节码并不针对一种特定的机器，因此，Java 程序无须重新编译便可在多种不同操作系统的计算机上运行。

Java 程序从源代码到运行一般有下面 3 步：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114170453562.png" alt="image-20210114170453562" style="zoom:50%;" />



我们需要格外注意的是 .class->机器码 这一步。

- 在这一步 JVM 类加载器首先加载字节码文件，然后通过解释器逐行解释执行，这种方式的执行速度会相对比较慢。而且，有些方法和代码块是经常需要被调用的(也就是所谓的热点代码)，所以后面引进了` JIT 编译器`，而 JIT 属于运行时编译。当 JIT 编译器完成第一次编译后，其会将字节码对应的机器码保存下来，下次可以直接使用。而我们知道，机器码的运行效率肯定是高于 Java 解释器的。这也解释了我们为什么经常会说 Java 是编译与解释共存的语言
- HotSpot 采用了惰性评估(`Lazy Evaluation`)的做法，根据二八定律，消耗大部分系统资源的只有那一小部分的代码（热点代码），而这也就是 JIT 所需要编译的部分。JVM 会根据代码每次被执行的情况收集信息并相应地做出一些优化，因此执行的次数越多，它的速度就越快。JDK 9 引入了一种新的编译模式 `AOT`(Ahead of Time Compilation)，它是直接将字节码编译成机器码，这样就避免了 `JIT 预热`等各方面的开销。JDK 支持分层编译和` AOT `协作使用。但是 ，AOT 编译器的编译质量是肯定比不上 JIT 编译器的。

总结

- Java 虚拟机（JVM）是运行 Java 字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），目的是使用相同的字节码，它们都会给出相同的结果。字节码和不同系统的 JVM 实现是 Java 语言“一次编译，随处可以运行”的关键所在

2、JDK 和 JRE

- JDK 是 Java Development Kit，它是功能齐全的 Java SDK。它拥有 JRE 所拥有的一切，还有编译器（javac）和工具（如 javadoc 和 jdb）。它能够创建和编译程序。


- 
  JRE 是 Java 运行时环境。它是运行已编译 Java 程序所需的所有内容的集合，包括 Java 虚拟机（JVM），Java 类库，java 命令和其他的一些基础构件。但是，它不能用于创建新程序。


- 如果你只是为了运行一下 Java 程序的话，那么你只需要安装 JRE 就可以了。如果你需要进行一些 Java 编程方面的工作，那么你就需要安装 JDK 了。
  - 但是，这不是绝对的。有时，即使您不打算在计算机上进行任何 Java 开发，仍然需要安装 JDK。例如，如果要使用 JSP 部署 Web 应用程序，那么从技术上讲，您只是在应用程序服务器中运行 Java 程序。那你为什么需要 JDK 呢？因为应用程序服务器会将 JSP 转换为 Java servlet，并且需要使用 JDK 来编译 servlet。

#### 1.3. Oracle JDK 和 OpenJDK 的对比


OpenJDK 项目主要基于 Sun 捐赠的 HotSpot 源代码。此外，OpenJDK 被选为 Java 7 的参考实现，由 Oracle 工程师维护

OpenJDK 存储库中的源代码与用于构建 Oracle JDK 的代码之间有什么区别？

- 非常接近 - 我们的 Oracle JDK 版本构建过程基于 OpenJDK 7 构建，只添加了几个部分，例如部署代码，其中包括 Oracle 的 Java 插件和 Java WebStart 的实现，以及一些封闭的源代码派对组件，如图形光栅化器，一些开源的第三方组件，如 Rhino，以及一些零碎的东西，如附加文档或第三方字体。展望未来，我们的目的是开源 Oracle JDK 的所有部分，除了我们考虑商业功能的部

总结
- Oracle JDK 大概每 6 个月发一次主要版本，而 OpenJDK 版本大概每三个月发布一次。但这不是固定的。详情参见：[https://blogs.oracle.com/java-platform-group/update-and-faq-on-the-java-se-release-cadence](https://blogs.oracle.com/java-platform-group/update-and-faq-on-the-java-se-release-cadence) 。
    - LTS 长期支持版本
- OpenJDK 是一个参考模型并且是完全开源的，而 Oracle JDK 是 OpenJDK 的一个实现，并不是完全开源的；
- Oracle JDK 比 OpenJDK 更稳定。OpenJDK 和 Oracle JDK 的代码几乎相同，但 Oracle JDK 有更多的类和一些错误修复。因此，如果您想开发企业/商业软件，我建议您选择 Oracle JDK，因为它经过了彻底的测试和稳定。某些情况下，有些人提到在使用 OpenJDK 可能会遇到了许多应用程序崩溃的问题，但是，只需切换到 Oracle JDK 就可以解决问题；
- 在响应性和 JVM 性能方面，Oracle JDK 与 OpenJDK 相比提供了更好的性能；
- Oracle JDK 根据二进制代码许可协议获得许可，而 OpenJDK 根据 GPL v2 许可获得许可。


相关问题
- OpenJDK和OracleJDK版本区别
    - OpenJDK是JDK的开放源码版本，以GPL协议的形式发布（General Public License）
    - Oracle JDK采用了商业实现
- LTS 是啥意思？
    - Long Term Support 长期支持的版本，如JDK8、JDK11都是属于LTS
    - JDK9 和 JDK10 这两个被称为“功能性的版本”不同, 两者均只提供半年的技术支持
    - 甲骨文释出Java的政策，每6个月会有一个版本的释出，长期支持版本每三年发布一次，根据后续的发布计划，下一个长期支持版 Java 17 将于2021年发布
- 8u20、11u20是啥意思？
    - 就是Java的补丁，比如JDK8的 8u20版本、8u60版本; java11的 11u20、11u40版本
- JDK要收费了？？？？
    - 问题的产生由来
        - Oracle 宣布 Java8 在 2019 年 1月之后停止更新，另外 Java11 及以后版本将不再提供免费的 long-term support (LTS) 支持，猜测未来将有越来越多 Java 开发者转向使用OpenJDK
        - OpenJDK是免费的，想要不断体验新特性的developer来说是不错的选择
        - OracleJDK不是免费的，对于企业用户来说，有钱的情况下就选择OracleJDK
    - 对应oracleJDK ,我们可以自己用来写代码，调试，学习即可

#### 1.4. Java 和 C++的区别

- 都是面向对象的语言，都支持封装、继承和多态
- Java 不提供指针来直接访问内存，程序内存更加安全
- Java 的类是单继承的，C++ 支持多重继承；虽然 Java 的类不可以多继承，但是接口可以多继承。
- Java 有自动内存管理机制，不需要程序员手动释放无用内存
- 在 C 语言中，字符串或字符数组最后都会有一个额外的字符‘\0’来表示结束。但是，Java 语言中没有结束符这一概念。

#### 1.5. 什么是 Java 程序的主类? 应用程序和小程序的主类有何不同?

一个程序中可以有多个类，但只能有一个类是主类。主类是 Java 程序执行的入口点。

- 在 Java 应用程序中，这个主类是指包含 main（）方法的类。
- 在 Java 小程序中，这个主类是一个继承自系统类 JApplet 或 Applet 的子类。应用程序的主类不一定要求是 public 类，但小程序的主类要求必须是 public 类。

#### 1.6. Java 应用程序与小程序之间有哪些差别

简单说应用程序是从主线程启动(也就是main()方法)。applet 小程序没有main()方法，主要是嵌在浏览器页面上运行(调用init()或者run()来启动)，嵌入浏览器这点跟 flash 的小游戏类似。

#### 1.7. import java 和 javax 有什么区别？

- 刚开始的时候 JavaAPI 所必需的包是 java 开头的包，javax 当时只是扩展 API 包来使用。然而随着时间的推移，javax 逐渐地扩展成为 Java API 的组成部分。但是，将扩展从 javax 包移动到 java 包确实太麻烦了，最终会破坏一堆现有的代码。因此，最终决定 javax 包将成为标准 API 的一部分。


- 所以，实际上 java 和 javax 没有区别。这都是一个名字。

#### 1.8. 为什么说 Java 语言“编译与解释并存”？

高级编程语言按照程序的执行方式分为编译型和解释型两种。
- 简单来说，编译型语言是指编译器针对特定的操作系统将源代码一次性翻译成可被该平台执行的机器码；解释型语言是指解释器对源程序逐行解释成特定平台的机器码并立即执行。比如，你想阅读一本英文名著，你可以找一个英文翻译人员帮助你阅读， 有两种选择方式，你可以先等翻译人员将全本的英文名著（也就是源码）都翻译成汉语，再去阅读，也可以让翻译人员翻译一段，你在旁边阅读一段，慢慢把书读完。

- Java 语言既具有编译型语言的特征，也具有解释型语言的特征，因为 Java 程序要经过先编译，后解释两个步骤，由 Java 编写的程序需要先经过编译步骤，生成字节码（*.class 文件），这种字节码必须由 Java 解释器来解释执行。因此，我们可以认为 Java 语言编译与解释并存。

### 2. 基础语法

#### 2.1. 字符型常量和字符串常量

字符型常量和字符串常量的区别

- 形式上: 字符常量是单引号引起的一个字符; 字符串常量是双引号引起的若干个字符
- 含义上: 字符常量相当于一个整型值( ASCII 值),可以参加表达式运算; 字符串常量代表一个地址值(该字符串在内存中存放位置)
```java
char a = 'a';
int sum = a + 1;
```
- 占内存大小 字符常量只占 2 个字节; 字符串常量占若干个字节 (注意： char 在 Java 中占两个字节)

#### 2.2. 短路运算符和位运算

1、按位(或|)、(与&)运算

- 按位运算符 `与&` 和  `或|` 需转成二进制进行运算

- & 按位与操作
  - 只有对应的两个二进制数为1时，结果位才为1    

```
1&1 = 1    
1&0 = 0    
0&1 = 0    
0&0 = 0
```
15&1  =》 1110&0000 =》 0000 = 1     

- | 按位或操作
  - 有一个为1的时候，结果位就为1    

```
1|1 = 1    
1|0 = 1    
0|1 = 1    
0|0 = 0
```

2、短路运算符 && 和 ||

- 短路运算符 && 和 ||，在逻辑判断中常见

- & 和 && 都可以实现"和"这个功能
  - 区别：& 两边都运算，而 && 先算 && 左侧，若左侧为false 那么右侧就不运算，判断语句中推荐使用 &&，效率更高

- | 和 || 和上面类似，都可以实现"或"这个功能
  - 区别：||只要满足第一个条件，后面的条件就不再判断，而|要对所有的条件进行判断

3、移位运算符

- <<(左移)、>>(右移)
    - 左移几位表示乘以2的几次方
    - 右移几位表示除以2的几次方

- 用最有效率的方法计算2乘以8
    - 原理：将一个数左移n位，相当于乘以2的n次方，位运算是CPU直接支持的，所以效率高
    - 答案：2<<3    0000 0010 左移3为  0001 0000  2- 2^3 即 左移3位 结果为16
        - 向左移动几位，表示乘以2的几次方
- 常见的JDK源码里面HashMap的默认容量16
    - `int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16`
    - 直接是二进制操作了，表示1左移4位，变成10000，转为10进制也就是16, 直接以二进制形式去运行，效率更高


#### 2.3. 关于注释

Java 中的注释有三种：

- 单行注释
- 多行注释
- 文档注释

在我们编写代码的时候，如果代码量比较少，我们自己或者团队其他成员还可以很轻易地看懂代码，但是当项目结构一旦复杂起来，我们就需要用到注释了。注释并不会执行，是我们程序员写给自己看的，注释是你的代码说明书，能够帮助看代码的人快速地理清代码之间的逻辑关系。因此，在写程序的时候随手加上注释是一个非常好的习惯

《Clean Code》这本书明确指出：
>代码的注释不是越详细越好。实际上好的代码本身就是注释，我们要尽量规范和美化自己的代码来减少不必要的注释。
>若编程语言足够有表达力，就不需要注释，尽量通过代码来阐述。

举个例子：去掉下面复杂的注释，只需要创建一个与注释所言同一事物的函数即可
```java
// check to see if the employee is eligible for full benefits 
if ((employee.flags & HOURLY_FLAG) && (employee.age > 65))
```
应替换为
```java
if (employee.isEligibleForFullBenefits())
```


#### 2.4. 标识符和关键字的区别

- 在我们编写程序的时候，需要大量地为程序、类、变量、方法等取名字，于是就有了标识符，简单来说，标识符就是一个名字。
- 但是有一些标识符，Java 语言已经赋予了其特殊的含义，只能用于特定的地方，这种特殊的标识符就是关键字。因此，关键字是被赋予特殊含义的标识符。比如，在我们的日常生活中 ，“警察局”这个名字已经被赋予了特殊的含义，所以如果你开一家店，店的名字不能叫“警察局”，“警察局”就是我们日常生活中的关键字。


#### 2.5. 自增自减运算符

在写代码的过程中，常见的一种情况是需要某个整数类型变量增加 1 或减少 1，Java 提供了一种特殊的运算符，用于这种表达式，叫做自增运算符（++)和自减运算符（--）。
- ++和--运算符可以放在操作数之前，也可以放在操作数之后，当运算符放在操作数之前时，先自增/减，再赋值；当运算符放在操作数之后时，先赋值，再自增/减。
- 例如，当“b=++a”时，先自增（自己增加 1），再赋值（赋值给 b）；当“b=a++”时，先赋值(赋值给 b)，再自增（自己增加 1）。也就是，++a 输出的是 a+1 的值，a++输出的是 a 值。
- 用一句口诀就是：“符号在前就先加/减，符号在后就后加/减”。


#### 2.6. continue、break、和return的区别

在循环结构中，当循环条件不满足或者循环次数达到要求时，循环会正常结束。但是，有时候可能需要在循环的过程中，当发生了某种条件之后 ，提前终止循环，这就需要用到下面几个关键词：

-  `continue` ：指跳出当前的这一次循环，继续下一次循环。
- `break` ：指跳出整个循环体，继续执行循环下面的语句。
- `return` 用于跳出所在方法，结束该方法的运行。return 一般有两种用法：
    - `return;`：直接使用 return 结束方法执行，用于没有返回值函数的方法
    -  `return value;`：return 一个特定值，用于有返回值函数的方法


#### 2.7. == 和 equals 的区别

1、`==`

它的作用是判断两个对象的地址是不是相等。即判断两个对象是不是同一个对象。(基本数据类型==比较的是值，引用数据类型==比较的是内存地址)

>因为 Java 只有值传递，所以，对于 == 来说，不管是比较基本数据类型，还是引用数据类型的变量，其本质比较的都是值，只是引用类型变量存的值是对象的地址。

2、`equals()`

它的作用也是判断两个对象是否相等，它不能用于比较基本数据类型的变量。equals()方法存在于Object类中，而Object类是所有类的直接或间接父类。


Object类equals()方法：

```java
public boolean equals(Object obj) {
     return (this == obj);
}
```

- equals()方法存在两种使用情况
    - 情况 1：类没有覆盖equals()方法。则通过equals()比较该类的两个对象时，等价于通过“==”比较这两个对象。使用的默认是Object类equals()方法。
    - 情况 2：类覆盖了equals()方法。一般，我们都覆盖equals()方法来两个对象的内容相等；若它们的内容相等，则返回 true(即，认为这两个对象相等)。

3、例子

```java
public class test1 {
    public static void main(String[] args) {
        String a = new String("ab"); // a 为一个引用
        String b = new String("ab"); // b为另一个引用,对象的内容一样
        String aa = "ab"; // 放在常量池中
        String bb = "ab"; // 从常量池中查找
        if (aa == bb) // true
            System.out.println("aa==bb");
        if (a == b) // false，非同一对象
            System.out.println("a==b");
        if (a.equals(b)) // true
            System.out.println("aEQb");
        if (42 == 42.0) { // true
            System.out.println("true");
        }
    }}
```
- 说明
    - String中的equals方法是被重写过的，因为Object的equals方法是比较的对象的内存地址，而String的equals方法比较的是对象的值。
    - 当创建`String类型的常量`时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引用。如果没有就在常量池中重新创建一个String对象。

- `String`类`equals()`方法：

```java
public boolean equals(Object anObject) {
    if (this == anObject) {
        return true;
    }
    if (anObject instanceof String) {
        String anotherString = (String)anObject;
        int n = value.length;
        if (n == anotherString.value.length) {
            char v1[] = value;
            char v2[] = anotherString.value;
            int i = 0;
            while (n-- != 0) {
                if (v1[i] != v2[i])
                    return false;
                i++;
            }
            return true;
        }
    }
    return false;
}
```


#### 2.8. hashCode()与 equals()

面试官可能会问你：“你重写过hashcode和equals么，为什么重写equals时必须重写hashCode方法？”

1、`hashCode()`介绍

- `hashCode()`的作用是获取哈希码，也称为散列码；它实际上是返回一个 int 整数。
  - 这个哈希码的作用是确定该对象在哈希表中的索引位置。
  - hashCode()定义在 JDK 的Object类中，这就意味着 Java 中的任何类都包含有hashCode()函数。另外需要注意的是：Object的 hashcode 方法是本地方法，也就是用 c 语言或 c++ 实现的，<u>该方法通常用来将对象的内存地址转换为整数之后返回</u>。

```java
public native int hashCode();
```

2、为什么要有 hashCode

- 散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）

- 我们以“HashSet如何检查重复”为例子来说明为什么要有 hashCode？
  - 当你把对象加入HashSet时，<u>HashSet会先计算对象的 hashcode 值来判断对象加入的位置</u>，同时也会与其他已经加入的对象的 hashcode 值作比较，如果没有相符的 hashcode，HashSet会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调用 equals（）方法来检查 hashcode 相等的对象是否真的相同。如果两者相同，HashSet就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。

3、为什么重写equals时必须重写hashCode方法

- 如果两个对象相等，则 hashcode 一定也是相同的。两个对象相等,对两个对象分别调用 equals 方法都返回 true。但是，两个对象有相同的 hashcode 值，它们也不一定是相等的 。因此，equals 方法被覆盖过，则hashCode方法也必须被覆盖。
- hashCode()的默认行为是对堆上的对象产生独特值。如果没有重写hashCode()，则该 class 的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）

4、为什么两个对象有相同的 hashcode 值，它们也不一定是相等的

- 因为hashCode()所使用的杂凑算法也许刚好会让多个对象传回相同的杂凑值。越糟糕的杂凑算法越容易碰撞(也就是我们所说的哈希碰撞)，但这也与数据值域分布的特性有关（所谓碰撞也就是指的是不同的对象得到相同的hashCode)。


- 我们刚刚也提到了HashSet,如果HashSet在对比的时候，同样的 hashcode 有多个对象，它会使用equals()来判断是否真的相同。也就是说<u>hashcode只是用来缩小查找成本</u>。


### 3. 方法（函数）

#### 3.1. 方法的返回值

方法的返回值是指我们获取到的某个方法体中的代码执行后产生的结果！（前提是该方法可能产生结果）。返回值的作用是接收出结果，使得它可以用于其他的操作！


#### 3.2. 为什么 Java 中只有值传递

在程序设计语言中有关将参数传递给方法（或函数）的一些专业术语

- 按值调用(call by value)表示方法接收的是调用者提供的值（参数值的一个拷贝）
- 按引用调用（call by reference)表示方法接收的是调用者提供的变量地址

一个方法可以修改传递引用所对应的变量值，而不能修改传递值调用所对应的变量值。 它用来描述各种程序设计语言（不只是 Java)中方法参数传递方式。

Java 程序设计语言总是采用按值调用。也就是说，<u>方法得到的是所有参数值的一个拷贝</u>，也就是说，方法不能修改传递给它的任何参数变量的内容。

1、example 1:  一个方法不能修改一个基本数据类型的参数

```java
public static void main(String[] args) {
    int num1 = 10;
    int num2 = 20;

    swap(num1, num2);

    System.out.println("num1 = " + num1);
    System.out.println("num2 = " + num2);}

public static void swap(int a, int b) {
    int temp = a;
    a = b;
    b = temp;

    System.out.println("a = " + a);
    System.out.println("b = " + b);}
```

结果：

```java
a = 20
b = 10
num1 = 10
num2 = 20
```

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114173928687.png" alt="image-20210114173928687" style="zoom:67%;" />


在 swap 方法中，a、b 的值进行交换，并不会影响到 num1、num2。因为，a、b 中的值，只是从 num1、num2 的复制过来的。也就是说，a、b 相当于 num1、num2 的副本，副本的内容无论怎么修改，都不会影响到原件本身。

我们已经知道了一个方法不能修改一个基本数据类型的参数，而对象引用作为参数就不一样，请看 example2.

2、example 2 对象引用作为参数

```java
public static void main(String[] args) {
    int[] arr = { 1, 2, 3, 4, 5 };
    System.out.println(arr[0]);
    change(arr);
    System.out.println(arr[0]);
}

public static void change(int[] array) {
    // 将数组的第一个元素变为0
    array[0] = 0;
}
```

结果：
```java
1
0
```

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114174011599.png" alt="image-20210114174011599" style="zoom:67%;" />

array 被初始化 arr 的拷贝也就是一个对象的引用，也就是说 array 和 arr 指向的是同一个数组对象。 因此，外部对引用对象的改变会反映到所对应的对象上。

通过 example2 我们已经看到，实现一个改变对象参数状态的方法并不是一件难事。理由很简单，方法得到的是对象引用的拷贝，对象引用及其他的拷贝同时引用同一个对象。

很多程序设计语言（特别是，C++和 Pascal)提供了两种参数传递的方式：值调用和引用调用。有些程序员（甚至本书的作者）认为 Java 程序设计语言对对象采用的是引用调用，实际上，这种理解是不对的。由于这种误解具有一定的普遍性，所以下面给出一个反例来详细地阐述一下这个问题。

3、example 3

```java
public class Test {

    public static void main(String[] args) {
        // TODO Auto-generated method stub
        Student s1 = new Student("小张");
        Student s2 = new Student("小李");
        Test.swap(s1, s2);
        System.out.println("s1:" + s1.getName());
        System.out.println("s2:" + s2.getName());
    }

    public static void swap(Student x, Student y) {
        Student temp = x;
        x = y;
        y = temp;
        System.out.println("x:" + x.getName());
        System.out.println("y:" + y.getName());
    }
}
```

结果：
```
x:小李
y:小张
s1:小张
s2:小李
```

解析：

交换之前：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114174041893.png" alt="image-20210114174041893" style="zoom:67%;" />

交换之后：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114174109453.png" alt="image-20210114174109453" style="zoom:67%;" />


通过上面两张图可以很清晰的看出：方法并没有改变存储在变量 s1 和 s2 中的对象引用。swap 方法的参数 x 和 y 被初始化为两个对象引用的拷贝，这个方法交换的是这两个拷贝


总结 Java 程序设计语言对对象采用的不是引用调用，实际上，对象引用是按值传递的。

下面再总结一下 Java 中方法参数的使用情况：

* 一个方法不能修改一个基本数据类型的参数（即数值型或布尔型）。
* 一个方法可以改变一个对象类型的方法入参的状态（对象参数引用的对象的状态）。
* 一个方法不能让对象类型的方法入参引用一个新的对象（值传递，不能修改对象参数的引用地址）。


#### 3.3. 重载和重写

重载就是同样的一个方法能够根据输入数据的不同，做出不同的处理

重写就是当子类继承自父类的相同方法，输入数据一样，但要做出有别于父类的响应时，你就要覆盖父类方法

1、重载

发生在同一个类中，方法名必须相同，参数类型不同、个数不同、顺序不同，方法返回值和访问修饰符可以不同。

重载就是同一个类中多个同名方法根据不同的传参来执行不同的逻辑处理。

2、重写发生在运行期

重写发生在运行期，是子类对父类的允许访问的方法的实现过程进行重新编写。

- 返回值类型、方法名、参数列表必须相同，抛出的异常范围小于等于父类，访问修饰符范围大于等于父类。
- 如果父类方法访问修饰符为`private/final/static`则子类就不能重写该方法，但是被 `static` 修饰的方法能够被再次声明。
- 构造方法无法被重写


综上：重写就是子类对父类方法的重新改造，外部样子不能改变，内部逻辑可以改变


#### 3.4. 深拷贝 vs 浅拷贝


* 浅拷贝：对基本数据类型进行值传递，对引用数据类型进行引用传递般的拷贝，此为浅拷贝。
* 深拷贝：对基本数据类型进行值传递，对引用数据类型，创建一个新的对象，并复制其内容，此为深拷贝。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114174206539.png" alt="image-20210114174206539" style="zoom:67%;" />



#### 3.5. 方法的四种类型

- 无参数无返回值的方法
- 有参数无返回值的方法
- 有返回值无参数的方法
- 有返回值有参数的方法


return 在无返回值方法的特殊使用

```java
// return在无返回值方法的特殊使用
public void f5(int a) {
    if (a>10) {
    return;//表示结束所在方法 （f5方法）的执行,下方的输出语句不会执行}
    System.out.println(a);
}
```

### 4. 类和对象

#### 4.1. 面向对象和面向过程

面向对象和面向过程的区别

- 面向过程 ：面向过程性能比面向对象高 因为类调用时需要实例化，开销比较大，比较消耗资源，所以当性能是最重要的考量因素的时候，比如单片机、嵌入式开发、Linux/Unix 等一般采用面向过程开发。但是，面向过程没有面向对象易维护、易复用、易扩展。

- 面向对象 ：面向对象易维护、易复用、易扩展。 因为面向对象有封装、继承、多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活、更加易于维护。但是，面向对象性能比面向过程低。

> 这个并不是根本原因，面向过程也需要分配内存，计算内存偏移量，Java 性能差的主要原因并不是因为它是面向对象语言，而是 Java 是半编译语言，最终的执行代码并不是可以直接被 CPU 执行的二进制机械码。

> 而面向过程语言大多都是直接编译成机械码在电脑上执行，并且其它一些面向过程的脚本语言性能也并不一定比 Java 好。

#### 4.2. 相关问题

1、构造器 Constructor 是否可被 override

Constructor 不能被 override（重写）,但是可以 overload（重载）,所以你可以看到一个类中有多个构造函数的情况。

2、在 Java 中定义一个不做事且没有参数的构造方法的作用

Java 程序在执行子类的构造方法之前，如果没有显示的用 `super()`来调用父类特定的构造方法，则默认会隐式的调用父类中“没有参数的构造方法”。

因此，如果父类中只定义了有参数的构造方法，而在子类的构造方法中又没有用 `super()`来调用父类中特定的构造方法，则编译时将发生错误，因为 Java 程序在父类中找不到没有参数的构造方法可供执行。解决办法是在父类里加上一个不做事且没有参数的构造方法。

3、成员变量与局部变量的区别

- 从语法形式上看:成员变量是属于类的，而局部变量是在方法中定义的变量或是方法的参数；成员变量可以被 public,private,static 等修饰符所修饰，而局部变量不能被访问控制修饰符及 static 所修饰；<u>但是，成员变量和局部变量都能被 final 所修饰</u>。

- 从变量在内存中的存储方式来看:如果成员变量是使用`static`修饰的，那么这个成员变量是属于类的，如果没有使用`static`修饰，这个成员变量是属于实例的。而对象存在于堆内存，局部变量则存在于栈内存。

- 从变量在内存中的生存时间上看:成员变量是对象的一部分，它随着对象的创建而存在，而局部变量随着方法的调用而自动消失。

- 成员变量如果没有被赋初值:则会自动以类型的默认值而赋值（一种情况例外:被 final 修饰的成员变量也必须显式地赋值），而局部变量则不会自动赋值。

4、创建一个对象用什么运算符?对象实体与对象引用有何不同?

new 运算符，new 创建对象实例（对象实例在堆内存中），对象引用指向对象实例（对象引用存放在栈内存中）。一个对象引用可以指向 0 个或 1 个对象（一根绳子可以不系气球，也可以系一个气球）;一个对象可以有 n 个引用指向它（可以用 n 条绳子系住一个气球）。

5、一个类的构造方法的作用是什么? 若一个类没有声明构造方法，该程序能正确执行吗? 为什么?

- 主要作用是完成对类对象的初始化工作。
- 若一个类没有声明构造方法，该程序可以执行。因为一个类即使没有声明构造方法也会有默认的不带参数的构造方法。
- 如果我们自己添加了类的构造方法（无论是否有参），Java 就不会再添加默认的无参数的构造方法了，这时候，就不能直接 new 一个对象而不传递参数了，所以我们一直在不知不觉地使用构造方法，这也是为什么我们在创建对象的时候后面要加一个括号（因为要调用无参的构造方法）。如果我们重载了有参的构造方法，记得都要把无参的构造方法也写出来（无论是否用到），因为这可以帮助我们在创建对象的时候少踩坑。

6、构造方法有哪些特性

1. 名字与类名相同。
2. 没有返回值，但不能用 void 声明构造函数。
3. 生成类的对象时自动执行，无需调用。

7、在调用子类构造方法之前会先调用父类没有参数的构造方法,其目的是?

默认会调用父类的 `super()` 构造方法，帮助子类做初始化工作。

8、对象的相等与指向他们的引用相等,两者有什么不同

对象的相等，比的是内存中存放的内容是否相等。而引用相等，比较的是他们指向的内存地址是否相等。

#### 4.3. 面向对象三大特征

1、封装

封装是指把一个对象的状态信息（也就是属性）隐藏在对象内部，不允许外部对象直接访问对象的内部信息。但是可以提供一些可以被外界访问的方法来操作属性。

就好像我们看不到挂在墙上的空调的内部的零件信息（也就是属性），但是可以通过遥控器（方法）来控制空调。如果属性不想被外界访问，我们大可不必提供方法给外界访问。但是如果一个类没有提供给外界访问的方法，那么这个类也没有什么意义了。就好像如果没有空调遥控器，那么我们就无法操控空凋制冷，空调本身就没有意义了（当然现在还有很多其他方法 ，这里只是为了举例子）。

```java
public class Student {
    private int id;//id属性私有化
    private String name;//name属性私有化

    //获取id的方法
    public int getId() {
        return id;
    }

    //设置id的方法
    public void setId(int id) {
        this.id = id;
    }

    //获取name的方法
    public String getName() {
        return name;
    }

    //设置name的方法
    public void setName(String name) {
        this.name = name;
    }
}
```

2、继承

不同类型的对象，相互之间经常有一定数量的共同点。例如，小明同学、小红同学、小李同学，都共享学生的特性（班级、学号等）。同时，每一个对象还定义了额外的特性使得他们与众不同。例如小明的数学比较好，小红的性格惹人喜爱；小李的力气比较大。继承是使用已存在的类的定义作为基础建立新类的技术，新类的定义可以增加新的数据或新的功能，也可以用父类的功能，但不能选择性地继承父类。通过使用继承，可以快速地创建新的类，可以提高代码的重用，程序的可维护性，节省大量创建新类的时间 ，提高我们的开发效率。

关于继承如下 3 点请记住：

1. <u>子类拥有父类对象所有的属性和方法（包括私有属性和私有方法），但是父类中的私有属性和方法子类是无法访问，只是拥有</u>。
2. 子类可以拥有自己属性和方法，即子类可以对父类进行扩展。
3. 子类可以用自己的方式实现父类的方法。

3、多态

多态，顾名思义，表示一个对象具有多种的状态。具体表现为父类的引用指向子类的实例。

多态的特点:

- 对象类型和引用类型之间具有继承（类）/实现（接口）的关系；
- 对象类型不可变，引用类型可变；
- 方法具有多态性，属性不具有多态性；
- 引用类型变量发出的方法调用的到底是哪个类中的方法，必须在程序运行期间才能确定；
- 多态不能调用“只在子类存在但在父类不存在”的方法；
- 如果子类重写了父类的方法，真正执行的是子类覆盖的方法，如果子类没有覆盖父类的方法，执行的是父类的方法。

### 5. 修饰符

#### 5.1. 修饰符相关问题

1、在一个静态方法内调用一个非静态成员为什么是非法的?

由于静态方法可以不通过对象进行调用，因此在静态方法里，不能调用其他非静态变量，也不可以访问非静态变量成员。

2、静态方法和实例方法有何不同

- 在外部调用静态方法时，可以使用"类名.方法名"的方式，也可以使用"对象名.方法名"的方式。而实例方法只有后面这种方式。也就是说，调用静态方法可以无需创建对象。

- 静态方法在访问本类的成员时，只允许访问静态成员（即静态成员变量和静态方法），而不允许访问实例成员变量和实例方法；实例方法则无此限制。


#### 5.2. 常见关键字 static,final,this,super

1、final 关键字

final关键字，意思是最终的、不可修改的，最见不得变化 ，用来修饰类、方法和变量，具有以下特点

- final修饰的类不能被继承，final类中的所有成员方法都会被隐式的指定为final方法；
- final修饰的方法不能被重写；
- final修饰的变量是常量，如果是基本数据类型的变量，则其数值一旦在初始化之后便不能更改；如果是引用类型的变量，则在对其初始化之后便不能让其指向另一个对象。

说明：使用final方法的原因有两个。<u>第一个原因是把方法锁定，以防任何继承类修改它的含义</u>；第二个原因是效率。在早期的Java实现版本中，会将final方法转为内嵌调用。但是如果方法过于庞大，可能看不到内嵌调用带来的任何性能提升（现在的Java版本已经不需要使用final方法进行这些优化了）。类中所有的private方法都隐式地指定为final。

2、static 关键字

static 关键字主要有以下四种使用场景：

- 修饰成员变量和成员方法: 
    - 被 static 修饰的成员属于类，不属于单个这个类的某个对象，被类中所有对象共享，可以并且建议通过类名调用。被static 声明的成员变量属于静态成员变量，静态变量存放在 Java 内存区域的方法区。调用格式：`类名.静态变量名` `类名.静态方法名()`
- 静态代码块: 
    - 静态代码块定义在类中方法外, 静态代码块在非静态代码块之前执行(静态代码块—>非静态代码块—>构造方法)。 
    - 该类不管创建多少对象，静态代码块只执行一次.
- 静态内部类（static修饰类的话只能修饰内部类）：
    - 静态内部类与非静态内部类之间存在一个最大的区别: <u>非静态内部类在编译完成之后会隐含地保存着一个引用，该引用是指向创建它的外围类，但是静态内部类却没有</u>。没有这个引用就意味着：1. 它的创建是不需要依赖外围类的创建。2. 它不能使用任何外围类的非static成员变量和方法。
- 静态导包(用来导入类中的静态资源，1.5之后的新特性):
    - 格式为：`import static` 这两个关键字连用可以指定导入某个类中的指定静态资源，并且不需要使用类名调用类中静态成员，可以直接使用类中静态成员变量和成员方法。

3、this 关键字

this关键字用于引用类的当前实例。 例如：

```java
class Manager {
    Employees[] employees;
     
    void manageEmployees() {
        int totalEmp = this.employees.length;
        System.out.println("Total employees: " + totalEmp);
        this.report();
    }
     
    void report() { }
}
```

在上面的示例中，this关键字用于两个地方：

- this.employees.length：访问类Manager的当前实例的变量。
- this.report（）：调用类Manager的当前实例的方法。

此关键字是可选的，这意味着如果上面的示例在不使用此关键字的情况下表现相同。 但是，使用此关键字可能会使代码更易读或易懂。

4、super 关键字

super关键字用于从子类访问父类的变量和方法。 例如：

```java
public class Super {
    protected int number;
     
    protected showNumber() {
        System.out.println("number = " + number);
    }
}
 
public class Sub extends Super {
    void bar() {
        super.number = 10;
        super.showNumber();
    }
}
```

在上面的例子中，Sub 类访问父类成员变量 number 并调用其其父类 Super 的 `showNumber（）` 方法。

使用 this 和 super 要注意的问题
- 在构造器中使用 `super（）` 调用父类中的其他构造方法时，<u>该语句必须处于构造器的首行</u>，否则编译器会报错。另外，this 调用本类中的其他构造方法时，也要放在首行。
- this、super不能用在static方法中。
    - 被 static 修饰的成员属于类，不属于单个这个类的某个对象，被类中所有对象共享。而 this 代表对本类对象的引用，指向本类对象；而 super 代表对父类对象的引用，指向父类对象；所以， this和super是属于对象范畴的东西，而静态方法是属于类范畴的东西。

#### 5.3. static 关键字详解

static 关键字主要有以下四种使用场景

- 修饰成员变量和成员方法
- 静态代码块
- 修饰类(只能修饰内部类)
- 静态导包(用来导入类中的静态资源，1.5之后的新特性)

1、修饰成员变量和成员方法(常用)

被 static 修饰的成员属于类，不属于单个这个类的某个对象，被类中所有对象共享，可以并且建议通过类名调用。被static 声明的成员变量属于静态成员变量，<u>静态变量 存放在 Java 内存区域的方法区</u>。

- 方法区与 Java 堆一样，是各个线程共享的内存区域，它用于存储已被虚拟机加载的类信息、常量、静态变量、即时编译器编译后的代码等数据。虽然Java虚拟机规范把方法区描述为堆的一个逻辑部分，但是它却有一个别名叫做 Non-Heap（非堆），目的应该是与 Java 堆区分开来。
-  HotSpot 虚拟机中方法区也常被称为 “永久代”，本质上两者并不等价。仅仅是因为 HotSpot 虚拟机设计团队用永久代来实现方法区而已，这样 HotSpot 虚拟机的垃圾收集器就可以像管理 Java 堆一样管理这部分内存了。但是这并不是一个好主意，因为这样更容易遇到内存溢出问题。

调用格式：

- `类名.静态变量名`
- `类名.静态方法名()`

如果变量或者方法被 private 则代表该属性或者该方法只能在类的内部被访问而不能在类的外部被访问。

测试方法：

```java
public class StaticBean {

    String name;
    //静态变量
    static int age;

    public StaticBean(String name) {
        this.name = name;
    }
    //静态方法
    static void SayHello() {
        System.out.println("Hello i am java");
    }
    @Override
    public String toString() {
        return "StaticBean{"+
                "name=" + name + ",age=" + age +
                "}";
    }
}
```

```java
public class StaticDemo {

    public static void main(String[] args) {
        StaticBean staticBean = new StaticBean("1");
        StaticBean staticBean2 = new StaticBean("2");
        StaticBean staticBean3 = new StaticBean("3");
        StaticBean staticBean4 = new StaticBean("4");
        StaticBean.age = 33;
        System.out.println(staticBean + " " + staticBean2 + " " + staticBean3 + " " + staticBean4);
        //StaticBean{name=1,age=33} StaticBean{name=2,age=33} StaticBean{name=3,age=33} StaticBean{name=4,age=33}
        StaticBean.SayHello();//Hello i am java
    }

}
```

2、静态代码块

静态代码块定义在类中方法外，静态代码块在非静态代码块之前执行(静态代码块—非静态代码块—构造方法)。该类不管创建多少对象，静态代码块只执行一次.

静态代码块的格式是 

```
static {    
语句体;   
}
```


一个类中的静态代码块可以有多个，位置可以随便放，它不在任何的方法体内，JVM加载类时会执行这些静态的代码块，如果静态代码块有多个，<u>JVM将按照它们在类中出现的先后顺序依次执行它们</u>，每个代码块只会被执行一次。

<img src="http://my-blog-to-use.oss-cn-beijing.aliyuncs.com/18-9-14/88531075.jpg" style="zoom:80%;" />

静态代码块对于定义在它之后的静态变量，可以赋值，但是不能访问.

3、静态内部类

静态内部类与非静态内部类之间存在一个最大的区别，我们知道非静态内部类在编译完成之后会隐含地保存着一个引用，该引用是指向创建它的外围类，但是静态内部类却没有。没有这个引用就意味着：

- 它的创建是不需要依赖外围类的创建。
- 它不能使用任何外围类的非static成员变量和方法。


Example（静态内部类实现单例模式）

```java
public class Singleton {
    
    //声明为 private 避免调用默认构造方法创建对象
    private Singleton() {
    }
    
   // 声明为 private 表明静态内部该类只能在该 Singleton 类中被访问
    private static class SingletonHolder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getUniqueInstance() {
        return SingletonHolder.INSTANCE;
    }
}
```

- 当 Singleton 类加载时，静态内部类 `SingletonHolder` 没有被加载进内存。只有当调用 `getUniqueInstance() `方法从而触发 `SingletonHolder.INSTANCE` 时 `SingletonHolder` 才会被加载，此时初始化 INSTANCE 实例，并且 JVM 能确保 INSTANCE 只被实例化一次。
- 这种方式不仅具有延迟初始化的好处，而且由 JVM 提供了对线程安全的支持。

4、静态导包

格式为：`import static `

这两个关键字连用可以指定导入某个类中的指定静态资源，<u>并且不需要使用类名调用类中静态成员，可以直接使用类中静态成员变量和成员方法</u>

```java


 //将Math中的所有静态资源导入，这时候可以直接使用里面的静态方法，而不用通过类名进行调用
 //如果只想导入单一某个静态方法，只需要将换成对应的方法名即可
 
import static java.lang.Math.*;//换成import static java.lang.Math.max;具有一样的效果
 
public class Demo {
  public static void main(String[] args) {
 
    int max = max(1,2);
    System.out.println(max);
  }
}

```


####  5.4. 补充内容

1、静态方法与非静态方法

静态方法属于类本身，非静态方法属于从该类生成的每个对象。 如果您的方法执行的操作不依赖于其类的各个变量和方法，请将其设置为静态（这将使程序的占用空间更小）。 否则，它应该是非静态的。

Example

```java
class Foo {
    int i;
    public Foo(int i) { 
       this.i = i;
    }

    public static String method1() {
       return "An example string that doesn't depend on i (an instance variable)";
       
    }

    public int method2() {
       return this.i + 1;  //Depends on i
    }

}
```
你可以像这样调用静态方法：`Foo.method1()`。 如果您尝试使用这种方法调用 `method2` 将失败。 但这样可行：`Foo bar = new Foo(1);  bar.method2();`

总结：

- 在外部调用静态方法时，可以使用”类名.方法名”的方式，也可以使用”对象名.方法名”的方式。而实例方法只有后面这种方式。也就是说，调用静态方法可以无需创建对象。 
- 静态方法在访问本类的成员时，只允许访问静态成员（即静态成员变量和静态方法），而不允许访问实例成员变量和实例方法；实例方法则无此限制 

2、`static{}`静态代码块与`{}`非静态代码块(构造代码块)

相同点： 都是在JVM加载类时且在构造方法执行之前执行，在类中都可以定义多个，定义多个时按定义的顺序执行，一般在代码块中对一些static变量进行赋值。 

不同点： 静态代码块在非静态代码块之前执行(静态代码块—非静态代码块—构造方法)。静态代码块在第一次new之前执行一次，之后不再执行，而非静态代码块在每new一次就执行一次。 非静态代码块可在普通方法中定义(不过作用不大)；而静态代码块不行。 

> 修正 [issue #677](https://github.com/Snailclimb/JavaGuide/issues/677)：静态代码块可能在第一次new的时候执行，但不一定只在第一次new的时候执行。比如通过 `Class.forName("ClassDemo")` 创建 Class 对象的时候也会执行。

一般情况下,如果有些代码比如一些项目最常用的变量或对象必须在项目启动的时候就执行的时候,需要使用静态代码块,这种代码是主动执行的。如果我们想要设计不需要创建对象就可以调用类中的方法，例如：Arrays类，Character类，String类等，就需要使用静态方法, 两者的区别是 静态代码块是自动执行的而静态方法是被调用的时候才执行的. 

Example：

```java
public class Test {
    public Test() {
        System.out.print("默认构造方法！--");
    }

    //非静态代码块
    {
        System.out.print("非静态代码块！--");
    }

    //静态代码块
    static {
        System.out.print("静态代码块！--");
    }

    private static void test() {
        System.out.print("静态方法中的内容! --");
        {
            System.out.print("静态方法中的代码块！--");
        }

    }

    public static void main(String[] args) {
        Test test = new Test();
        Test.test();//静态代码块！--静态方法中的内容! --静态方法中的代码块！--
    }
}
```

上述代码输出：

```
静态代码块！--非静态代码块！--默认构造方法！--静态方法中的内容! --静态方法中的代码块！--
```

当只执行 `Test.test();` 时输出：

```
静态代码块！--静态方法中的内容! --静态方法中的代码块！--
```

当只执行 `Test test = new Test();` 时输出：

```
静态代码块！--非静态代码块！--默认构造方法！--
```


非静态代码块与构造函数的区别是：非静态代码块是给所有对象进行统一初始化，而构造函数是给对应的对象初始化，因为构造函数是可以多个的，运行哪个构造函数就会建立什么样的对象，但无论建立哪个对象，都会先执行相同的构造代码块。也就是说，构造代码块中定义的是不同对象共性的初始化内容。 

### 6. 接口和抽象类

#### 6.1. 接口和抽象类的区别

- 接口的方法默认是 `public`，所有方法在接口中不能有实现(Java 8 开始接口方法可以有默认实现），而抽象类可以有非抽象的方法。
- 接口中除了 `static`、`final` 变量，不能有其他变量，且变量必须由 `public` 访问修饰。而抽象类中则不一定。
- 一个类可以实现多个接口，但只能实现一个抽象类。接口自己本身可以通过 `extends` 关键字扩展多个接口。
- 接口方法默认修饰符是 `public abstract`，抽象方法可以有 `public`、`protected` 和 `default`  这些修饰符（抽象方法就是为了被重写所以不能使用 `private` 关键字修饰！）。
- 从设计层面来说，抽象是对类的抽象，是一种模板设计，而接口是对行为的抽象，是一种行为的规范。


#### 6.2. jdk7~jdk9 接口概念的变化

总结一下 jdk7~jdk9 Java 中接口概念的变化（[相关阅读](https://www.geeksforgeeks.org/private-methods-java-9-interfaces/)）：

1、jdk7：抽象方法

在 jdk 7 或更早版本中，接口里面只能有 `public` 修饰的公共的常量/静态变量(`static`、`final` 变量)和抽象方法( `public abstract` )。这些接口方法必须由选择实现接口的类实现。

<u>在接口中定义一个抽象方法时，`public abstract` 可以省略</u>。

2、jdk8：公共的默认方法、公共静态方法

jdk8 的时候接口可以有`public default` 公共的默认方法和 公共静态方法 `public static` 功能。

- `public default` 公共默认方法 ，默认方法表示接口对该方法的默认实现。 
    - 实现接口时默认方法可以不进行重写。
    - 通过接口实现类的对象.默认方法调用
    - 如果同时实现两个接口，接口中都定义了一样的默认方法，则必须重写，不然会报错
- `public static` 公共静态方法
    - 通过接口名.静态方法可以调用
    - 不能通过实现类调用的

```java
// Java 8 program to illustrate 
// static, default and abstract methods in interfaces 
public interface TempI { 

	public abstract void div(int a, int b); 

    public default void add(int a, int b)  { 
		System.out.print("Answer by Default method = "); 
		System.out.println(a + b); 
	} 

	public static void mul(int a, int b)  { 
		System.out.print("Answer by Static method = "); 
		System.out.println(a * b); 
	} 
} 

class Temp implements TempI { 

	@Override
	public void div(int a, int b) { 
		System.out.print("Answer by Abstract method = "); 
		System.out.println(a / b); 
	} 

	public static void main(String[] args) 
	{ 
		TempI in = new Temp(); 
		in.div(8, 2); 
		in.add(3, 1); 
		TempI.mul(4, 1); 
	} 
} 

```

3、jdk9：私有方法、私有静态方法

Jdk 9 在接口中引入了私有方法和私有静态方法。

- 私有方法： `private`  私有方法定义了默认实现，只能在当前接口里面调用
- 私有静态方法 ` private static`  私有静态方法定义了默认实现，只能在当前接口内调用

```java
// Java 9 program to illustrate 
// private methods in interfaces 
public interface TempI { 

	public abstract void mul(int a, int b); 

	public default void add(int a, int b)  { 
	// private method inside default method 
		sub(a, b); 

	// static method inside other non-static method 
		div(a, b); 
		System.out.print("Answer by Default method = "); 
		System.out.println(a + b); 
	} 

	public static void mod(int a, int b) { 
		div(a, b); // static method inside other static method 
		System.out.print("Answer by Static method = "); 
		System.out.println(a % b); 
	} 

	private void sub(int a, int b)  { 
		System.out.print("Answer by Private method = "); 
		System.out.println(a - b); 
	} 

	private static void div(int a, int b) { 
		System.out.print("Answer by Private static method = "); 
		System.out.println(a / b); 
	} 
} 

class Temp implements TempI { 

	@Override
	public void mul(int a, int b) 
	{ 
		System.out.print("Answer by Abstract method = "); 
		System.out.println(a * b); 
	} 

	public static void main(String[] args) 
	{ 
		TempI in = new Temp(); 
		in.mul(2, 3); 
		in.add(6, 2); 
		TempI.mod(5, 3); 
	} 
} 
```

### 7. 异常

#### 7.1. Java 异常类层次结构图

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114182047750.png" alt="image-20210114182047750" style="zoom:50%;" />

在 Java 中，所有的异常都有一个共同的祖先 java.lang 包中的 Throwable 类。Throwable： 有两个重要的子类：Exception（异常） 和 Error（错误） ，二者都是 Java 异常处理的重要子类，各自都包含大量子类。

- Error（错误）是程序无法处理的错误，表示运行应用程序中较严重问题
  - 大多数错误与代码编写者执行的操作无关，而<u>表示代码运行时 JVM（Java 虚拟机）出现的问题</u>。例如，Java 虚拟机运行错误（Virtual MachineError），当 JVM 不再有继续执行操作所需的内存资源时，将出现 `OutOfMemoryError`。这些异常发生时，Java 虚拟机（JVM）一般会选择线程终止。
  - 这些错误表示故障发生于虚拟机自身、或者发生在虚拟机试图执行应用时，如 Java 虚拟机运行错误（Virtual MachineError）、类定义错误（NoClassDefFoundError）等。这些错误是不可查的，因为它们在应用程序的控制和处理能力之 外，而且绝大多数是程序运行时不允许出现的状况。对于设计合理的应用程序来说，即使确实发生了错误，本质上也不应该试图去处理它所引起的异常状况。在 Java 中，错误通过 Error 的子类描述。

- Exception（异常）:是程序本身可以捕获并处理的异常。
  - Exception 类有一个重要的子类 RuntimeException。RuntimeException 异常由 Java 虚拟机抛出。
  - NullPointerException（要访问的变量没有引用任何对象时，抛出该异常）、ArithmeticException（算术运算异常，一个整数除以 0 时，抛出该异常）和 ArrayIndexOutOfBoundsException（下标越界异常）。

- 注意：异常和错误的区别：异常能被程序本身处理，错误是无法处理。

#### 7.2. Throwable 类常用方法

- `public string getMessage()`:返回异常发生时的简要描述
- `public string toString()`:返回异常发生时的详细信息
- `public string getLocalizedMessage()`:返回异常对象的本地化信息。使用 `Throwable` 的子类覆盖这个方法，可以生成本地化信息。如果子类没有覆盖该方法，则该方法返回的信息与 `getMessage（）`返回的结果相同
- `public void printStackTrace()`:在控制台上打印 `Throwable` 对象封装的异常信息（堆栈信息）


#### 7.3. try-catch-finally

try 块：用于捕获异常。其后可接零个或多个 catch 块，如果没有 catch 块，则必须跟一个 finally 块。

catch 块：用于处理 try 捕获到的异常。

finally 块：无论是否捕获或处理异常(即是否有catch语句)，finally 块里的语句都会被执行。当在 try 块或 catch 块中遇到 return 语句时，<u>finally 语句块将在方法返回之前被执行</u>。

- 在以下 4 种特殊情况下，finally 块不会被执行：

  - 对于try-catch-finally或者try-finally，<u>如果不能进入try块，则finally块也无法进入</u>
  - 在前面的代码中用了System.exit(int)中止当前虚拟机，如果虚拟机被中止，程序也会被终止，finally代码块自然不会执行。
  - 程序所在的线程死亡
  - 关闭 CPU

注意： 当 try 语句和 finally 语句中都有 return 语句时，<u>在方法返回之前，finally 语句的内容将被执行，并且 finally 语句的返回值将会覆盖原始的返回值</u>。如下：

```java
public class Test {
    public static int f(int value) {
        try {
            return value * value;
        } finally {
            if (value == 2) {
                return 0;
            }
        }
    }
}
```

如果调用 `f(2)`，返回值将是 0，因为 finally 语句的返回值覆盖了 try 语句块的返回值。

详细执行过程如下：

1. 如果有返回值，就把返回值保存到局部变量中；
2. 执行jsr指令跳到finally语句里执行；
    1. 如果try，finally语句里均有return，忽略try的return，而使用finally的return.
3. 执行完finally语句后，返回之前保存在局部变量表里的值。


#### 7.4. 使用 `try-with-resources` 来代替 `try-catch-finally`

1. 适用范围（资源的定义）：任何实现 `java.lang.AutoCloseable` 或者 `java.io.Closeable` 的对象
2. 关闭资源和catch、finally的执行顺序：在 `try-with-resources` 语句中，任何 catch 或 finally 块在声明的资源关闭后再运行
3. 关闭多个资源顺序： 多个资源使用;进行分隔。资源的 close 方法调用顺序与它们的创建顺序相反
4. jdk 1.7 资源需要在try(...) 中进行声明并初始化。到了jdk1.9 增强的try-with-resources支持在try(...)外部声明初始化资源，之后把该资源添加到try中即可。

《Effecitve Java》中明确指出：

> 面对必须要关闭的资源，我们总是应该优先使用 `try-with-resources` 而不是`try-finally`。随之产生的代码更简短，更清晰，产生的异常对我们也更有用。`try-with-resources`语句让我们更容易编写必须要关闭的资源的代码，若采用`try-finally`则几乎做不到这点。

Java 中类似于`InputStream`、`OutputStream` 、`Scanner` 、`PrintWriter`等的资源都需要我们调用`close()`方法来手动关闭，一般情况下我们都是通过`try-catch-finally`语句来实现这个需求，如下：

```java
//读取文本文件的内容
Scanner scanner = null;
try {
    scanner = new Scanner(new File("D://read.txt"));
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException e) {
    e.printStackTrace();
} finally {
    if (scanner != null) {
        scanner.close();
    }
}
```

使用Java 7之后的 `try-with-resources` 语句改造上面的代码:

```java
try (Scanner scanner = new Scanner(new File("test.txt"))) {
    while (scanner.hasNext()) {
        System.out.println(scanner.nextLine());
    }
} catch (FileNotFoundException fnfe) {
    fnfe.printStackTrace();
}
```

当然多个资源需要关闭的时候，使用 `try-with-resources`  实现起来也非常简单，如果你还是用`try-catch-finally`可能会带来很多问题。

通过使用分号分隔，可以在`try-with-resources`块中声明多个资源。资源的 close 方法调用顺序与它们的创建顺序相反

```java
try (BufferedInputStream bin = new BufferedInputStream(new FileInputStream(new File("test.txt")));
             BufferedOutputStream bout = new BufferedOutputStream(new FileOutputStream(new File("out.txt")))) {
            int b;
            while ((b = bin.read()) != -1) {
                bout.write(b);
            }
        }
        catch (IOException e) {
            e.printStackTrace();
        }
```

增强try-with-resource。在JDK9中，改进了try-with-resources语句，在try外进行初始化，在括号内引用，即可实现资源自动关闭，多个变量则用分号进行分割

```java
public static void main(String[] args) throws Exception {
    String path = "/Users/xdclass/Desktop/t.txt";
    test(path);
}
private static void test(String filepath) throws FileNotFoundException {
    OutputStream out = new FileOutputStream(filepath);
    try (out) {
        out.write((filepath + "可以学习java架构课程").getBytes());
    } catch (Exception e) {
        e.printStackTrace();
    }
}
```
不需要在try中声明资源 `out` 就可以使用它，并得到相同的结果

### 8. 其它重要知识点

#### 8.1. String、StringBuffer 和 StringBuilder 的区别

1、String 为什么是不可变的?

简单的来说：`String` 类中使用` final`关键字修饰字符数组来保存字符串，`private final char value[]`，所以` String` 对象是不可变的。

> 补充（来自[issue 675](https://github.com/Snailclimb/JavaGuide/issues/675)）：在 Java 9 之后，String 类的实现改用 `byte` 数组存储字符串 `private final byte[] value`;

2、StringBuffer 和 StringBuilder 的区别

而 `StringBuilder` 与 `StringBuffer` 都继承自 `AbstractStringBuilder` 类，在 `AbstractStringBuilder` 中也是使用字符数组保存字符串`char[] value` 但是没有用 `final` 关键字修饰，所以这两种对象都是可变的。

`StringBuilder` 与 `StringBuffer` 的构造方法都是调用父类构造方法也就是`AbstractStringBuilder` 实现的，大家可以自行查阅源码。

`AbstractStringBuilder.java`

```java
abstract class AbstractStringBuilder implements Appendable, CharSequence {
    /**
     * The value is used for character storage.
     */
    char[] value;

    /**
     * The count is the number of characters used.
     */
    int count;

    AbstractStringBuilder(int capacity) {
        value = new char[capacity];
    }}
```

- 线程安全性
    - `String` 中的对象是不可变的，也就可以理解为常量，线程安全。
    - `AbstractStringBuilder` 是 `StringBuilder` 与 `StringBuffer` 的公共父类，定义了一些字符串的基本操作，如 `expandCapacity`、`append`、`insert`、`indexOf` 等公共方法。
        - `StringBuffer` 对方法加了`synchronized` 同步锁或者对调用的方法加了同步锁，所以是线程安全的。
        - `StringBuilder` 并没有对方法进行加同步锁，所以是非线程安全的。

- 性能
    - 每次对 `String` 类型进行改变的时候，都会生成一个新的 `String` 对象，然后将指针指向新的 `String` 对象。
    - `StringBuffer` 每次都会对 `StringBuffer` 对象本身进行操作，而不是生成新的对象并改变对象引用。
    - 相同情况下使用 `StringBuilder` 相比使用 `StringBuffer` 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的风险。

3、对于三者使用的总结

- 操作少量的数据: 适用 `String`
- 单线程操作字符串缓冲区下操作大量数据: 适用 `StringBuilder`
- 多线程操作字符串缓冲区下操作大量数据: 适用 `StringBuffer`


#### 8.2. Object 类的常见方法总结

Object 类是一个特殊的类，是所有类的父类。它主要提供了以下 11 个方法：

```java

//native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。
public final native Class<?> getClass()

//native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的HashMap。
public native int hashCode()

//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。
public boolean equals(Object obj)

//naitive方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass() == x.getClass() 为true。Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。
protected native Object clone() throws CloneNotSupportedException

//返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方法。
public String toString()

//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
public final native void notify()

//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
public final native void notifyAll()

//native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。
public final native void wait(long timeout) throws InterruptedException

//多了nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上nanos毫秒。
public final void wait(long timeout, int nanos) throws InterruptedException

//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念
public final void wait() throws InterruptedException

//实例被垃圾回收器回收的时候触发的操作
protected void finalize() throws Throwable { }

```

#### 8.3. == 与 equals

== : 它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不是同一个对象(基本数据类型比较的是值，引用数据类型比较的是内存地址)。

equals() : 它的作用也是判断两个对象是否相等。但它一般有两种使用情况：

- 情况 1：类没有覆盖 equals() 方法。则通过 equals() 比较该类的两个对象时，等价于通过“==”比较这两个对象。
- 情况 2：类覆盖了 equals() 方法。一般，我们都覆盖 equals() 方法来比较两个对象的内容是否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

举个例子：

```java
public class test1 {
    public static void main(String[] args) {
        String a = new String("ab"); // a 为一个引用
        String b = new String("ab"); // b为另一个引用,对象的内容一样
        String aa = "ab"; // 放在常量池中
        String bb = "ab"; // 从常量池中查找
        if (aa == bb) // true
            System.out.println("aa==bb");
        if (a == b) // false，非同一对象
            System.out.println("a==b");
        if (a.equals(b)) // true
            System.out.println("aEQb");
        if (42 == 42.0) { // true
            System.out.println("true");
        }
    }
}
```

说明：

- String 中的 equals 方法是被重写过的，因为 object 的 equals 方法是比较的对象的内存地址，而 String 的 equals 方法比较的是对象的值。
- 当创建 String 类型的常量字符串(如上面所述的aa、bb)时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引用。如果没有就在常量池中重新创建一个 String 对象。


#### 8.4. hashCode 与 equals

面试官可能会问你：“你重写过 hashcode 和 equals 么，为什么重写 equals 时必须重写 hashCode 方法？”

1、hashCode（）介绍

hashCode() 的作用是获取哈希码，也称为散列码；它实际上是返回一个 int 整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。hashCode() 定义在 JDK 的 Object.java 中，这就意味着 Java 中的任何类都包含有 hashCode() 函数。

hashset、hashmap这些散列表存储的是键值对(key-value)，它的特点是：能根据“键”快速的检索出对应的“值”。这其中就利用到了散列码！（可以快速找到所需要的对象）

2、为什么要有 hashCode

我们先以“HashSet 如何检查重复”为例子来说明为什么要有 hashCode： 当你把对象加入 HashSet 时，HashSet 会先计算对象的 hashcode 值来判断对象加入的位置，同时也会与该位置其他已经加入的对象的 hashcode 值作比较，如果没有相符的 hashcode，HashSet 会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调用 `equals()`方法来检查 hashcode 相等的对象是否真的相同。如果两者相同，HashSet 就不会让其加入操作成功。如果不同的话，就会重新散列到其他位置。（摘自我的 Java 启蒙书《Head first java》第二版）。这样我们就大大减少了 equals 的次数，相应就大大提高了执行速度。

通过我们可以看出：`hashCode()` 的作用就是获取哈希码，也称为散列码；它实际上是返回一个 int 整数。这个哈希码的作用是确定该对象在哈希表中的索引位置。`hashCode()`在散列表中才有用，在其它情况下没用 。在散列表中 hashCode() 的作用是获取对象的散列码，进而确定该对象在散列表中的位置。

3、hashCode（）与 equals（）的相关规定

- 如果两个对象相等，则 hashcode 一定也是相同的
- 两个对象相等,对两个对象分别调用 equals 方法都返回 true
- 两个对象有相同的 hashcode 值，它们也不一定是相等的
- 因此，equals 方法被覆盖过，则 hashCode 方法也必须被覆盖
- hashCode() 的默认行为是对堆上的对象产生独特值。如果没有重写 hashCode()，则该 class 的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）

#### 8.5. Java 序列化中如果有些字段不想进行序列化，怎么办？

对于不想进行序列化的变量，使用` transient `关键字修饰。

`transient` 关键字的作用是：阻止实例中那些用此关键字修饰的的变量序列化；当对象被反序列化时，被 transient 修饰的变量值不会被持久化和恢复。transient 只能修饰变量，不能修饰类和方法。

#### 8.6. 获取用键盘输入常用的两种方法

方法 1：通过 `Scanner`

```java
Scanner input = new Scanner(System.in);
String s  = input.nextLine();
input.close();
```

方法 2：通过 `BufferedReader`

```java
BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
String s = input.readLine();
```



## 2-Java集合

### 1. 集合概述

#### 1.1. Java 集合概览

从下图可以看出，在 Java 中除了以 `Map` 结尾的类之外， 其他类都实现了 `Collection` 接口。

并且，以 `Map` 结尾的类都实现了 `Map` 接口。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114181046531.png" alt="image-20210114181046531" style="zoom:70%;" />

List,Set,Map 三者的区别？

- `List` (对付顺序的好帮手)： 存储的元素是有序的、可重复的。

- `Set` (注重独一无二的性质):  存储的元素是无序的、不可重复的。

- `Map` (用 Key 来搜索的专家): 使用键值对（kye-value）存储，类似于数学上的函数 y=f(x)，“x”代表 key，"y"代表 value，Key 是无序的、不可重复的，value 是无序的、可重复的，每个键最多映射到一个值。


#### 1.2. 集合框架底层数据结构

先来看一下 `Collection` 接口下面的集合。

1、`List`

- `Arraylist`： `Object[]`数组

- `Vector`：`Object[]`数组

- `LinkedList`： 双向链表(JDK1.6 之前为循环链表，JDK1.7 取消了循环，为双向链表)

2、`Set`

- `HashSet`（无序，唯一）: 基于 `HashMap` 实现的，底层采用 `HashMap` 来保存元素

- `LinkedHashSet`：`LinkedHashSet` 是 `HashSet` 的子类，其内部是通过 `LinkedHashMap` 来实现的

- `TreeSet`（有序，唯一）： 红黑树(自平衡的排序二叉树)，其内部是通过 `TreeMap` 来实现的。

3、`Map`

- `HashMap`： 
  - JDK1.8 之前 HashMap 由 数组+链表 组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）。
  - JDK1.8 以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以<u>减少搜索时间</u>
- `LinkedHashMap`： `LinkedHashMap` 继承自 `HashMap`，所以它的底层仍然是基于拉链式散列结构即由数组和链表或红黑树组成。另外，`LinkedHashMap` 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。
- `Hashtable`： 数组+链表 组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的
- `TreeMap`： 红黑树（自平衡的排序二叉树）

#### 1.3. 如何选用集合

主要根据集合的特点来选用

* 我们需要根据键值获取到元素值时就选用 `Map` 接口下的集合，需要排序时选择 `TreeMap`, 不需要排序时就选择 `HashMap`,需要保证线程安全就选用 `ConcurrentHashMap`。

* 当我们只需要存放元素值时，就选择实现 `Collection` 接口的集合，需要保证元素唯一时选择实现 `Set` 接口的集合比如 `TreeSet` 或 `HashSet`，不需要就选择实现 `List` 接口的比如 `ArrayList` 或 `LinkedList`，然后再根据实现这些接口的集合的特点来选用。


#### 1.4. 为什么要使用集合

当我们需要保存一组类型相同的数据的时候，我们应该是用一个容器来保存，这个容器就是数组，但是，使用数组存储对象具有一定的弊端，因为我们在实际开发中，存储的数据的类型是多种多样的，于是，就出现了“集合”，集合同样也是用来存储多个数据的。

数组的缺点是一旦声明之后，长度就不可变了；同时，声明数组时的数据类型也决定了该数组存储的数据的类型；而且，数组存储的数据是有序的、可重复的，特点单一。但是集合提高了数据存储的灵活性，Java 集合不仅可以用来存储不同类型不同数量的对象，还可以保存具有映射关系的数据

#### 1.5. Iterator 迭代器

1、迭代器 Iterator 是什么

```java
public interface Iterator<E> {
    //集合中是否还有元素
    boolean hasNext();
    //获得集合中的下一个元素
    E next();
    ......
}
```

- `Iterator` 对象称为迭代器（设计模式的一种），迭代器可以对集合进行遍历，但每一个集合内部的数据结构可能是不尽相同的，所以每一个集合存和取都很可能是不一样的，虽然我们可以人为地在每一个类中定义 `hasNext()` 和 `next()` 方法，但这样做会让整个集合体系过于臃肿。于是就有了迭代器。
- 迭代器是将这样的方法抽取出接口，然后<u>在每个类的内部，定义自己迭代方式</u>，这样做就规定了整个集合体系的遍历方式都是 `hasNext()`和`next()`方法，使用者不用管怎么实现的，会用即可。迭代器的定义为：提供一种方法访问一个容器对象中各个元素，而又不需要暴露该对象的内部细节。

2、迭代器 Iterator 有啥用

- `Iterator` 主要是用来遍历集合用的
- 它的特点是更加安全，因为它可以确保，在当前遍历的集合元素被更改的时候，就会抛出 `ConcurrentModificationException` 异常。

3、如何使用？

我们通过使用迭代器来遍历 `HashMap`，演示一下 迭代器 Iterator 的使用。

```java

Map<Integer, String> map = new HashMap();
map.put(1, "Java");
map.put(2, "C++");
map.put(3, "PHP");
Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
while (iterator.hasNext()) {
  Map.Entry<Integer, String> entry = iterator.next();
  System.out.println(entry.getKey() + entry.getValue());
}
```

#### 1.6. 有哪些集合是线程不安全的以及怎么解决

我们常用的 `Arraylist` ,`LinkedList`,`Hashmap`,`HashSet`,`TreeSet`,`TreeMap`，`PriorityQueue` 都不是线程安全的。解决办法很简单，可以使用线程安全的集合来代替。

- 如果你要使用线程安全的集合的话， `java.util.concurrent` 包中提供了很多并发容器供你使用：
  - `ConcurrentHashMap`: 可以看作是线程安全的 `HashMap`
  - `CopyOnWriteArrayList`: 可以看作是线程安全的 `ArrayList`，在读多写少的场合性能非常好，远远好于 `Vector`.
  - `ConcurrentLinkedQueue`:高效的并发队列，使用链表实现。可以看做一个线程安全的 `LinkedList`，这是一个非阻塞队列。
  - `BlockingQueue`: 这是一个接口，JDK 内部通过链表、数组等方式实现了这个接口。表示阻塞队列，非常适合用于作为数据共享的通道。
  - `ConcurrentSkipListMap` :跳表的实现。这是一个`Map`，使用跳表的数据结构进行快速查找。

### 2. List

#### 2.1. List 集合类

1、Arraylist 和 Vector 的区别

1. ArrayList 是 List 的主要实现类，底层使用 `Object[]`数组存储，适用于频繁的查找工作，线程不安全 ；
2. Vector 是 List 的古老实现类，底层使用 `Object[]`数组存储，<u>线程安全的</u>。

2、Arraylist 与 LinkedList 区别?

- 是否保证线程安全： `ArrayList` 和 `LinkedList` 都是不同步的，也就是不保证线程安全；
- 底层数据结构：`Arraylist` 底层使用的是`Object[]` 数组；数组是通过下标去操作的。`LinkedList` 底层使用的是 双向链表 数据结构，`LinkedList`当中的每一个元素为一个`Node`，`Node`对象里面保存它的直接前驱节点和直接后继节点
- 增删改查效率问题：
    - `ArrayList`：底层是数组实现，查询和修改非常快，但是增加和删除慢。数组是通过下标去操作的,查询和修改当前元素，直接通过下标即可找到并进行修改。在某一位置增加或者删除元素要移动后面的所有元素，效率很低。
    - `LinkedList`: 底层是双向链表，查询和修改速度慢，增加和删除速度快。查询得从第一个节点开始一个一个进行查询，查询到并进行修改。增加和删除速度快，增加或删除某一个给定的节点，直接改变节点当中的后继指针和前驱指针即可。
- 插入和删除是否受元素位置的影响：
    - `ArrayList` 采用数组存储，所以插入和删除元素的时间复杂度受元素位置的影响。 
      - 比如：执行`add(E e)`方法的时候， `ArrayList` 会默认在将指定的元素追加到此列表的末尾，这种情况时间复杂度就是 O(1)。
      - 但是如果要在指定位置 i 插入和删除元素的话（`add(int index, E element)`）时间复杂度就为 O(n-i)，最大时间复杂度O(n)。因为在进行上述操作的时候集合中第 i 和第 i 个元素之后的(n-i)个元素都要执行向后位/向前移一位的操作。
    - `LinkedList` 采用链表存储。 
      - 对于`add(E e)`方法的插入(插入尾部)或`remove(Object o)`删除元素，时间复杂度为 O(1)，不受元素位置的影响
      - 如果是要在指定位置`i`插入的话（`(add(int index, E element)`） 时间复杂度近似为`o(n))`。因为需要先移动到指定位置再插入

```java
ArrayList 是线性表（数组）
get() 直接读取第几个下标，复杂度 O(1)
add(E) 添加元素，直接在后面添加，复杂度O（1）
add(index, E) 添加元素，在第几个元素后面插入，后面的元素需要向后移动，复杂度O（n）
remove（）元素的删除，后面的元素需要逐个移动，复杂度O（n）

LinkedList 是链表的操作
get() 获取第几个元素，依次遍历，复杂度O(n)
add(E) 添加到末尾，复杂度O(1)
add(index, E) 添加第几个元素后，需要先查找到第几个元素，直接指针指向操作，复杂度O(n)
remove（）元素的删除，直接指针指向操作，复杂度O(1)
```

- 是否支持快速随机访问： `LinkedList` 不支持高效的随机元素访问，而 `ArrayList` 支持。快速随机访问就是通过元素的序号快速获取元素对象(对应于`get(int index)`方法)。

- 内存空间占用： ArrayList 的空间浪费主要体现在在 list 列表的结尾会预留一定的容量空间，而 LinkedList 的空间花费则体现在它的每一个元素都需要消耗比 ArrayList 更多的空间（因为要存放直接后继和直接前驱以及数据）。

- 是否有序： `ArrayList` 和 `LinkedList`  存储的元素都是有序的、可重复的。<u>默认顺序都为添加时的顺序</u>

3、补充内容：双向链表和双向循环链表

双向链表： 包含两个指针，一个 prev 指向前一个节点，一个 next 指向后一个节点。

> 另外推荐一篇把双向链表讲清楚的文章：[https://juejin.im/post/5b5d1a9af265da0f47352f14](https://juejin.im/post/5b5d1a9af265da0f47352f14)

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115085010917.png" alt="image-20210115085010917" style="zoom:60%;" />


双向循环链表： 最后一个节点的 next 指向 head节点，而 head 的 prev 指向最后一个节点，构成一个环。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115085030198.png" alt="image-20210115085030198" style="zoom:60%;" />

4、补充内容：`RandomAccess` 接口

```java
public interface RandomAccess {
}
```

查看源码我们发现实际上 `RandomAccess` 接口中什么都没有定义。所以，在我看来 `RandomAccess` 接口不过是一个标识罢了。标识什么？ 标识实现这个接口的类具有随机访问功能。

在 `binarySearch（)` 方法中，它要判断传入的 list 是否 `RamdomAccess` 的实例，如果是，调用`indexedBinarySearch()`方法，如果不是，那么调用`iteratorBinarySearch()`方法

```java
    public static <T>
    int binarySearch(List<? extends Comparable<? super T>> list, T key) {
        if (list instanceof RandomAccess || list.size()<BINARYSEARCH_THRESHOLD)
            return Collections.indexedBinarySearch(list, key);
        else
            return Collections.iteratorBinarySearch(list, key);
    }
```

`ArrayList` 实现了 `RandomAccess` 接口， 而 `LinkedList` 没有实现。为什么呢？还是和底层数据结构有关！`ArrayList` 底层是数组，而 `LinkedList` 底层是链表。数组天然支持随机访问，时间复杂度为 O(1)，所以称为快速随机访问。链表需要遍历所有位置才能访问特定位置的元素，时间复杂度为 O(n)，所以不支持快速随机访问。`ArrayList` 实现了 `RandomAccess` 接口，就表明了他具有快速随机访问功能。 `RandomAccess` 接口只是标识，并不是说 `ArrayList` 实现 `RandomAccess` 接口才具有快速随机访问功能的！

5、使用场景

* Vector已经很少用了
* 增加和删除场景多则用 `LinkedList`
* 查询和修改多则用 `ArrayList`

6、部分源码

ArrayList源码解析

* add方法没有任何的锁操作，非线程安全
* 扩容机制

```java
//点击add方法查看源码
new ArrayList<>().add("");

//add方法没有任何的锁操作，非线程安全
public boolean add(E e) {
    //确保容量
	ensureCapacityInternal(size + 1);  // Increments modCount!!
    //把元素放到数组最后一位
	elementData[size++] = e;
	return true;
}
```

LinkedList源码解析

* 非线程安全
* LinkedList当中的每一个元素为一个 `Node`，Node对象里面保存它的直接前驱节点和直接后继节点

```java
//点击add方法查看源码
new LinkedList<>().add("");

//add方法没有任何的锁操作，非线程安全
public boolean add(E e) {    
    linkLast(e);    
    return true;
}
//LinkedList当中的每一个元素为一个Node，Node对象里面保存它的直接前驱节点和直接后继节点
private static class Node<E> {
	E item;
	Node<E> next;
	Node<E> prev;

	Node(Node<E> prev, E element, Node<E> next) {
		this.item = element;
		this.next = next;
		this.prev = prev;
	}
}
```

Vector源码解析

* 使用 `synchronized` 进行加锁，线程安全，

```java
//点击add方法查看源码
new Vector<>().add("");

//add方法使用synchronized进行加锁，线程安全，效率比arrayList低
public synchronized boolean add(E e) {    
    modCount++;    
    ensureCapacityHelper(elementCount + 1);    
    elementData[elementCount++] = e;    
    return true;
}
```

#### 2.2. ArrayList

##### 1. 简介

ArrayList 的底层是数组队列，相当于动态数组。与 Java 中的数组相比，它的容量能动态增长。在添加大量元素前，应用程序可以使用`ensureCapacity`操作来增加 ArrayList 实例的容量。这可以减少递增式再分配的数量。

它继承于 AbstractList，实现了 List, RandomAccess, Cloneable, java.io.Serializable 这些接口。

在我们学数据结构的时候就知道了线性表的顺序存储，插入删除元素的时间复杂度为O（n）,求表长以及增加元素，取第 i 元素的时间复杂度为O（1）

- ArrayList 继承了`AbstractList`，实现了`List`。它是一个数组队列，提供了相关的添加、删除、修改、遍历等功能。


- ArrayList 实现了`RandomAccess` 接口， RandomAccess 是一个标志接口，表明实现这个这个接口的 List 集合是支持快速随机访问的。在 ArrayList 中，我们即可以通过元素的序号快速获取元素对象，这就是快速随机访问。


- ArrayList 实现了`Cloneable` 接口，即覆盖了函数 clone()，能被克隆。


- ArrayList 实现了`java.io.Serializable` 接口，这意味着ArrayList支持序列化，能通过序列化去传输。


- 和 Vector 不同，ArrayList 中的操作不是线程安全的！所以，建议在单线程中才使用 ArrayList，而在多线程中可以选择 `Vector` 或者  `CopyOnWriteArrayList`

##### 2. `System.arraycopy()` 和 `Arrays.copyOf()` 方法的使用

通过源码我们发现这两个实现数组复制的方法被广泛使用而且很多地方都特别巧妙。比如下面`add(int index, E element)`方法就很巧妙的用到了`arraycopy()`方法让数组自己复制自己实现让index开始之后的所有成员后移一个位置:
```java 
    /**
     * 在此列表中的指定位置插入指定的元素。 
     *先调用 rangeCheckForAdd 对index进行界限检查；然后调用 ensureCapacityInternal 方法保证capacity足够大；
     *再将从index开始之后的所有成员后移一个位置；将element插入index位置；最后size加1。
     */
    public void add(int index, E element) {
        rangeCheckForAdd(index);
        //确保容量
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        //arraycopy()方法实现数组自己复制自己
        //elementData:源数组;index:源数组中的起始位置;elementData：目标数组；index + 1：目标数组中的起始位置； size - index：要复制的数组元素的数量；
        System.arraycopy(elementData, index, elementData, index + 1, size - index);
        elementData[index] = element;
        size++;
    }
```
1、System.arraycopy用法：

```java
System.arraycopy(Object src, int srcPos, Object dest, int destPos,int length) 参数介绍
    * `Object src` : 原数组
    * `int srcPos` : 从原数据的起始位置开始
    * `Object dest` : 目标数组
    * `int destPos` : 目标数组的开始起始位置
    * `int length`  : 要copy的元数组的长度，从元数据的起始位置开始计算
```

2、Arrays.copyOf用法：

- toArray()方法中用到了copyOf()方法
- 从第一个元素开始进行复制，返回一个新的数组对象。

```java
    /**
     *以正确的顺序（从第一个到最后一个元素）返回一个包含此列表中所有元素的数组。 
     *返回的数组将是“安全的”，因为该列表不保留对它的引用。 （换句话说，这个方法必须分配一个新的数组）。
     *因此，调用者可以自由地修改返回的数组。 此方法充当基于阵列和基于集合的API之间的桥梁。
     */
    public Object[] toArray() {
    //elementData：要复制的数组；size：要复制的长度
        return Arrays.copyOf(elementData, size);
    }
```

3、两者联系与区别

- 联系：
  - 看两者源代码可以发现`copyOf()`内部调用了`System.arraycopy()`方法

- 区别：
  - arraycopy()需要目标数组，将原数组拷贝到你自己定义的数组里，而且可以选择拷贝的起点和长度以及放入新数组中的位置
  - copyOf()是系统自动在内部新建一个数组，并返回该数组。


##### 3. ArrayList 核心扩容技术

JDK1.7创建ArrayList对象之后默认容量大小是10，JDk1.7之后是 0

扩容机制:

- 创建ArrayList对象未指定集合容量，默认是0，若已经指定大小则集合大小为指定的；<u>创建的时候能指定容量最好，无需再去扩容，提高效率</u>。
- 当集合第一次添加元素的时候，集合大小需要扩容为10
- ArrayList的元素个数大于其容量时进行扩容，`扩容的大小= 原始大小+原始大小/2`。
  - 超过默认大小10之后再次扩容 `int newCapacity = oldCapacity + (oldCapacity >> 1);`

调试代码

```java
List<String> list = new ArrayList<>();
//添加10个元素，默认list第一次添加元素的时候，集合大小扩容为10
for(int i=0;i<10;i++){
    list.add(""+i);
}
System.out.println(list.size());

//添加第11个元素，元素个数大于其容量，进行扩容，此时容量为15，但是size为11。 size为容器当中的元素个数
list.add("xdclass.net");
System.out.println(list.size());
```

源码分析

```java

//当集合第一次添加元素的时候，集合大小默认为10
private static final int DEFAULT_CAPACITY = 10;

//集合创建时默认为空集合
private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

//集合size大小 第一次默认为0
private int size;

 //保存ArrayList数据的数组
transient Object[] elementData; // non-private to simplify nested class access

//创建ArrayList对象未指定集合容量，默认是空集合，集合容量为0
public ArrayList() {    
    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
}

//指定集合容量大小
public ArrayList(int initialCapacity) {
	if (initialCapacity > 0) {
		this.elementData = new Object[initialCapacity];
	} else if (initialCapacity == 0) {
		this.elementData = EMPTY_ELEMENTDATA;
	} else {
		throw new IllegalArgumentException("Illegal Capacity: "+ initialCapacity);
	}
}

//添加元素方法 第一次添加元素时 size为0
public boolean add(E e) {
	ensureCapacityInternal(size + 1);  // Increments modCount!!
	elementData[size++] = e;
	return true;
}

private void ensureCapacityInternal(int minCapacity) {
	ensureExplicitCapacity(calculateCapacity(elementData, minCapacity));
}

//计算容量，第一次添加元素时，集合为空集合，默认容量和初始容量比较，取最大值 Math.max(DEFAULT_CAPACITY, minCapacity) 初次添加时容量为DEFAULT_CAPACITY 10
private static int calculateCapacity(Object[] elementData, int minCapacity) {
	if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
		return Math.max(DEFAULT_CAPACITY, minCapacity);
	}
	return minCapacity;
}

//判断是否需要扩容
private void ensureExplicitCapacity(int minCapacity) {
    modCount++;
    // 如果说minCapacity也就是所需的最小容量大于保存ArrayList数据的数组的长度的话，就需要调用grow(minCapacity)方法扩容。
    //这个minCapacity到底为多少呢？举个例子在添加元素(add)方法中这个minCapacity的大小就为现在数组的长度加1
    if (minCapacity - elementData.length > 0)
        //调用grow方法进行扩容，调用此方法代表已经开始扩容了
        grow(minCapacity);
}

/**
 * ArrayList扩容的核心方法。
 */
private void grow(int minCapacity) {
   //elementData为保存ArrayList数据的数组
   //elementData.length求数组长度  而elementData.size是求数组中的元素个数
    // oldCapacity为ArrayList的旧容量，newCapacity为ArrayList的新容量    minCapacity为ArrayList所需的最少容量
    int oldCapacity = elementData.length;
    //将oldCapacity 右移一位，其效果相当于oldCapacity /2，
    //我们知道位运算的速度远远快于整除运算，整句运算式的结果就是将新容量更新为旧容量的1.5倍，
    int newCapacity = oldCapacity + (oldCapacity >> 1);
    //然后检查新容量是否大于最小需要容量，若还是小于最小需要容量，那么就把最小需要容量当作数组的新容量，
    if (newCapacity - minCapacity < 0)
        newCapacity = minCapacity;
    //再检查新容量是否超出了ArrayList所定义的最大容量，
    //若超出了，则调用hugeCapacity()来比较minCapacity和 MAX_ARRAY_SIZE，
    //如果minCapacity大于MAX_ARRAY_SIZE，则新容量则为Interger.MAX_VALUE，否则，新容量大小则为 MAX_ARRAY_SIZE。
    if (newCapacity - MAX_ARRAY_SIZE > 0)
        newCapacity = hugeCapacity(minCapacity);
    // minCapacity is usually close to size, so this is a win:
    elementData = Arrays.copyOf(elementData, newCapacity);
}

private static int hugeCapacity(int minCapacity) {
	if (minCapacity < 0) // overflow
		throw new OutOfMemoryError();
	return (minCapacity > MAX_ARRAY_SIZE) ?
		Integer.MAX_VALUE :
		MAX_ARRAY_SIZE;
} 
```
- 移位运算符
  - 简介：移位运算符就是在二进制的基础上对数字进行平移。按照平移的方向和填充数字的规则分为三种`<<`(左移)、`>>`(带符号右移)和`>>>`(无符号右移)。
  - 作用：对于大数据的2进制运算,位移运算符比那些普通运算符的运算要快很多,因为程序仅仅移动一下而已,不去计算,这样提高了效率,节省了资源
    - 比如这里`：int newCapacity = oldCapacity + (oldCapacity >> 1);`
      右移一位相当于除2，右移n位相当于除以 2 的 n 次方。这里 oldCapacity 明显右移了1位所以相当于oldCapacity /2。
    - 右移几位，相当于除以2的几次方，左移几位，相当于乘以2的几次方

- 另外需要注意的
  - java 中的length属性是针对数组说的,比如说你声明了一个数组,想知道这个数组的长度则用到了 length 这个属性. 表示数组大小（容量）

  - java 中的length()方法是针对字符串String说的,如果想看这个字符串的长度则用到 length()这个方法.

  - java 中的size()方法是针对泛型集合说的,如果想看这个泛型有多少个元素,就调用此方法来查看!

##### 4. 内部类

```java
(1)private class Itr implements Iterator<E>  
(2)private class ListItr extends Itr implements ListIterator<E>  
(3)private class SubList extends AbstractList<E> implements RandomAccess  
(4)static final class ArrayListSpliterator<E> implements Spliterator<E>  
```

ArrayList有四个内部类

- Itr是实现了Iterator接口，同时重写了里面的hasNext()， next()， remove() 等方法；
- ListItr 继承 Itr，实现了ListIterator接口，同时重写了hasPrevious()， nextIndex()， previousIndex()， previous()， set(E e)， add(E e) 等方法，
- 所以这也可以看出了 Iterator和ListIterator的区别: ListIterator在Iterator的基础上增加了添加对象，修改对象，逆向遍历等方法，这些是Iterator不能实现的。

#####  5. ArrayList保证线程安全

<u>问题: 如果需要保证线程安全，ArrayList应该怎么做，用有几种方式</u>

- 方式一：自己写个包装类，根据业务一般是add/update/remove加锁 

- 方式二：Collections.synchronizedList(new ArrayList<>());  对list对象进行封装，返回 `synchronizedList`，所有的操作使用synchronized加锁

```java
//返回SynchronizedList包装类对象，所有的操作进行了synchronized加锁。
List<String> list =  Collections.synchronizedList(new ArrayList<>());
list.add("aaa");
```
Collections.synchronizedList源码分析
```java
public static <T> List<T> synchronizedList(List<T> list) {
	return (list instanceof RandomAccess ?
			new SynchronizedRandomAccessList<>(list) :
			new SynchronizedList<>(list));
}

static class SynchronizedList<E> extends SynchronizedCollection<E> implements List<E> {
	...
	SynchronizedList(List<E> list) {
		super(list);
		this.list = list;
	}
	public E get(int index) {
		synchronized (mutex) {return list.get(index);}
	}
	public E set(int index, E element) {
		synchronized (mutex) {return list.set(index, element);}
	}
	...
}
```

- 方式三：CopyOnWriteArrayList<>()  
  - 底层数组实现，使用ReentrantLock加锁。get相关的读取操作不进行加锁，set相关的变更操作加锁
    - 每次拷贝到新的新数组里面，对新数组进行修改，并修改引用地址，指向新的数组对象
    - set之前原先get到的是一个旧的数组，里面没有新存放的数据。
  - 可以看作是线程安全的 `ArrayList`，在读多写少的场合性能非常好，远远好于 `Vector`.


```java
List<String> list =  new CopyOnWriteArrayList<>();
list.add("aaa");
```

CopyOnWriteArrayList源码
```java
package java.util.concurrent;

public class CopyOnWriteArrayList<E> implements List<E>, RandomAccess, Cloneable, java.io.Serializable {
	//get方法不加锁
    public E get(int index) {
        return get(getArray(), index);
    }
    //add方法加锁
	public boolean add(E e) {
        final ReentrantLock lock = this.lock;
        lock.lock();
        try {
            //获取旧的数组
            Object[] elements = getArray();
            //获取旧数组长度
            int len = elements.length;
            //拷贝到一个新的数组，新数组长度加1来存储最新的元素
            Object[] newElements = Arrays.copyOf(elements, len + 1);
            newElements[len] = e;
            //内存中有两块空间，修改引用地址，指向新的数组对象
            setArray(newElements);
            return true;
        } finally {
            lock.unlock();
        }
    }
}
```


##### 6. ArrayList排序

1、comparable 和 Comparator 的区别

- `comparable` 接口实际上是出自`java.lang`包。它有一个 `compareTo(Object obj)` 方法用来排序
  - 集合里面的元素实现`comparable` 接口，并重写 `compareTo(Object obj)` 方法
- `comparator` 接口实际上是出自 `java.util`包它有一个`compare(Object obj1, Object obj2)`方法用来排序
  - 创建实现`Comparator`接口的`comparator`对象，使用工具类`Collections.sort`进行排序

Comparator 定制排序

```java
ArrayList<Integer> arrayList = new ArrayList<Integer>();
arrayList.add(-1);
arrayList.add(3);
arrayList.add(3);
arrayList.add(-5);
arrayList.add(7);
arrayList.add(4);
arrayList.add(-9);
arrayList.add(-7);
System.out.println("原始数组:");
System.out.println(arrayList);
// void reverse(List list)：反转
Collections.reverse(arrayList);
System.out.println("Collections.reverse(arrayList):");
System.out.println(arrayList);

// void sort(List list),按自然排序的升序排序
Collections.sort(arrayList);
System.out.println("Collections.sort(arrayList):");
System.out.println(arrayList);
// 定制排序的用法
Collections.sort(arrayList, new Comparator<Integer>() {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2.compareTo(o1);
    }
});
System.out.println("定制排序后：");
System.out.println(arrayList);
```

Output:

```
原始数组:
[-1, 3, 3, -5, 7, 4, -9, -7]
Collections.reverse(arrayList):
[-7, -9, 4, 7, -5, 3, 3, -1]
Collections.sort(arrayList):
[-9, -7, -5, -1, 3, 3, 4, 7]
定制排序后：
[7, 4, 3, 3, -1, -5, -7, -9]
```

重写 compareTo 方法实现按年龄来排序

```java
// person对象没有实现Comparable接口，所以必须实现，这样才不会出错，才可以使treemap中的数据按顺序排列
// 前面一个例子的String类已经默认实现了Comparable接口，详细可以查看String类的API文档，另外其他
// 像Integer类等都已经实现了Comparable接口，所以不需要另外实现了
public  class Person implements Comparable<Person> {
    private String name;
    private int age;

    public Person(String name, int age) {
        super();
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    /**
     * T重写compareTo方法实现按年龄来排序 
     * 从小到大排序
     */
    @Override
    public int compareTo(Person o) {
        if (this.age > o.getAge()) {
            return 1;
        }
        if (this.age < o.getAge()) {
            return -1;
        }
        return 0;
    }
}

```

```java
    public static void main(String[] args) {
        TreeMap<Person, String> pdata = new TreeMap<Person, String>();
        pdata.put(new Person("张三", 30), "zhangsan");
        pdata.put(new Person("李四", 20), "lisi");
        pdata.put(new Person("王五", 10), "wangwu");
        pdata.put(new Person("小红", 5), "xiaohong");
        // 得到key的值的同时得到key所对应的值
        Set<Person> keys = pdata.keySet();
        for (Person key : keys) {
            System.out.println(key.getAge() + "-" + key.getName());

        }
    }
```

Output：

```
5-小红
10-王五
20-李四
30-张三
```

2、ArrayList排序算法->二分排序(二分法插入排序)

- 定义
  - 二分排序是指利用二分法的思想对插入排序进行改进的一种插入排序算法，不同于二叉排序，可以利用数组的特点快速定位指定索引的元素。
- 算法思想
  - 二分法插入排序是在插入第i个元素时，对前面的0～i-1元素进行折半，第i个元素先跟他们中间的那个元素比，如果小，则`对前半`再进行折半，否则`对后半`进行折半，直到`left>right`，然后再把第i个元素前1位与目标位置之间的所有元素后移，再把第i个元素放在目标位置上。
- 代码示例 `TimSort#sort`

```java
static <T> void sort(T[] a, int lo, int hi, Comparator<? super T> c,
					 T[] work, int workBase, int workLen) {
	assert c != null && a != null && lo >= 0 && lo <= hi && hi <= a.length;

	int nRemaining  = hi - lo;
	if (nRemaining < 2)
		return;  // Arrays of size 0 and 1 are always sorted  小于2不用排序,直接返回

	// If array is small, do a "mini-TimSort" with no merges
   //看是否小于min_merge,如果小于就直接二分排序,没必要进行复杂的timsort.
	if (nRemaining < MIN_MERGE) {
		int initRunLen = countRunAndMakeAscending(a, lo, hi, c);
		binarySort(a, lo, hi, lo + initRunLen, c);
		return;
	}

	/**
	 * March over the array once, left to right, finding natural runs,
	 * extending short natural runs to minRun elements, and merging runs
	 * to maintain stack invariant.
	 */
	TimSort<T> ts = new TimSort<>(a, c, work, workBase, workLen);
	int minRun = minRunLength(nRemaining);
	do {
		// Identify next run
		int runLen = countRunAndMakeAscending(a, lo, hi, c);

		// If run is short, extend to min(minRun, nRemaining)
		if (runLen < minRun) {
			int force = nRemaining <= minRun ? nRemaining : minRun;
			binarySort(a, lo, lo + force, lo + runLen, c);
			runLen = force;
		}

		// Push run onto pending-run stack, and maybe merge
		ts.pushRun(lo, runLen);
		ts.mergeCollapse();

		// Advance to find next run
		lo += runLen;
		nRemaining -= runLen;
	} while (nRemaining != 0);

	// Merge all remaining runs to complete sort
	assert lo == hi;
	ts.mergeForceCollapse();
	assert ts.stackSize == 1;
}
```

countRunAndMakeAscending找到a数组中从lo开始并且已经有序(递增或者递减)的元素个数,返回已经有序的元素个数.在这里如果降序在翻转一下,变为有序.

```java
private static <T> int countRunAndMakeAscending(T[] a, int lo, int hi,
												Comparator<? super T> c) {
	assert lo < hi;
	int runHi = lo + 1;
	if (runHi == hi)
		return 1;

	// Find end of run, and reverse range if descending
	if (c.compare(a[runHi++], a[lo]) < 0) { // Descending 降序 
		while (runHi < hi && c.compare(a[runHi], a[runHi - 1]) < 0)
			runHi++;
		reverseRange(a, lo, runHi);  //如果逆序在翻转一下,变为升序. [start,end)逆序不包括最右边界序号。
	} else {                              // Ascending 升序
		while (runHi < hi && c.compare(a[runHi], a[runHi - 1]) >= 0)
			runHi++;
	}
	return runHi - lo;
}
```
Comparator默认实现是a[runHi++].compareTo(a[lo])。如果c.compare(a[runHi++], a[lo])比较返回小于0即a[runHi++]<a[lo]，需要进行逆序翻转一下。整个数组按从小到大顺序排序。

如果重写了Comparator，实现为a[lo].compareTo(a[runHi++])。如果c.compare(a[runHi++], a[lo])比较返回小于0即a[lo]<a[runHi++]，需要进行逆序翻转一下。整个数组按从大到小顺序排序。

在进行查看二分排序源码时，假定Comparator的实现是按照从小到大排序。


```java
private static <T> void binarySort(T[] a, int lo, int hi, int start, Comparator<? super T> c) {
	assert lo <= start && start <= hi;
	if (start == lo)
		start++;
	for ( ; start < hi; start++) {
		T pivot = a[start];

		// Set left (and right) to the index where a[start] (pivot) belongs
		int left = lo;            //每次循环左边界默认为0
		int right = start;       //每次以start作为右边界值
		assert left <= right;
		/*
		 * Invariants:
		 *   pivot >= all in [lo, left).
		 *   pivot <  all in [right, start).
		 */
		while (left < right) {
          //计算中间下标值
			int mid = (left + right) >>> 1;
          //当前元素与中间下标值对于的元素进行比较，如果小于0则对前半再次进行折半，直到左边界=右边界
			if (c.compare(pivot, a[mid]) < 0)
				right = mid;  //元素值比中间值小，向左折半，right变小会接近left
			else
              //如果大于0则对后半进行折半，直到左边界=右边界
				left = mid + 1;  //元素值比中间值大，向右折半，left会变大接近right
		}
		assert left == right;  //这里是当左边界值等于右边界值的时候比较完成。因为当前要插入的元素的下标已参与到最右边界

		/*
		 * The invariants still hold: pivot >= all in [lo, left) and
		 * pivot < all in [left, start), so pivot belongs at left.  Note
		 * that if there are elements equal to pivot, left points to the
		 * first slot after them -- that's why this sort is stable.
		 * Slide elements over to make room for pivot.
		 */
		int n = start - left;  // The number of elements to move   需要移动元素的个数
		// Switch is just an optimization for arraycopy in default case
		switch (n) {
			case 2:  a[left + 2] = a[left + 1];
			case 1:  a[left + 1] = a[left];
					 break;
          //a:源数组; left:源数组中的起始位置;  a：目标数组；left + 1：目标数组中的起始位置； n：要复制的数组元素的数量；
			default: System.arraycopy(a, left, a, left + 1, n); //移动元素超过3个以上或者没有移动则执行该方法。
		}
		a[left] = pivot; //最小值赋值到最左边
	}
}
```
* `Object src` : 原数组
    * `int srcPos` : 从元数据的起始位置开始
    * `Object dest` : 目标数组
    * `int destPos` : 目标数组的开始起始位置
    * `int length`  : 要copy的元数组的长度，从元数据的起始位置开始计算

- 分析
  - 时间复杂度:  二分排序的时间复杂度是O(n^2)
  - 空间复杂度:  空间复杂度O(1)，是稳定排序。

##### 7. Arrays.asList()的使用

最近使用`Arrays.asList()`遇到了一些坑，对于这块小知识点进行了简单的总结。

1、简介

`Arrays.asList()`在平时开发中还是比较常见的，我们可以使用它将一个数组转换为一个List集合。

```java
String[] myArray = { "Apple", "Banana", "Orange" }； 
List<String> myList = Arrays.asList(myArray);
//上面两个语句等价于下面一条语句
List<String> myList = Arrays.asList("Apple","Banana", "Orange");
```

JDK 源码对于这个方法的说明：`Arrays`的内部类`ArrayList`


```java
/**
 *返回由指定数组支持的固定大小的列表。此方法作为基于数组和基于集合的API之间的桥梁，
 *与Collection.toArray()结合使用。返回的List是可序列化并实现RandomAccess接口。
 */ 
public static <T> List<T> asList(T... a) {
    return new ArrayList<>(a);
}
```

2、《阿里巴巴Java 开发手册》对其的描述

`Arrays.asList()`将数组转换为集合后,底层其实还是数组，《阿里巴巴Java 开发手册》对于这个方法有如下描述：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115091712843.png" alt="image-20210115091712843" style="zoom: 60%;" />

3、使用时的注意事项总结

- 传递的数组必须是对象数组，而不是基本类型。 
  - `Arrays.asList()`是泛型方法，传入的对象必须是`对象数组`。
  - 当传入一个原生数据类型(基本数据类型)数组时，`Arrays.asList()` 的真正得到的参数就不是数组中的元素，而是数组对象本身！此时List 的唯一元素就是这个数组，这也就解释了下面的代码。
  - 我们使用包装类型数组就可以解决这个问题

```java
int[] myArray = { 1, 2, 3 };
List myList = Arrays.asList(myArray);
System.out.println(myList.size());//1
System.out.println(myList.get(0));//数组地址值
System.out.println(myList.get(1));//报错：ArrayIndexOutOfBoundsException
int [] array=(int[]) myList.get(0);
System.out.println(array[0]);//1
```
```java
//我们使用包装类型数组就可以解决这个问题。
Integer[] myArray = { 1, 2, 3 };
```

- 使用集合的修改方法:`add()`、`remove()`、`clear()`会抛出异常。
  - `Arrays.asList()` 方法返回的并不是 `java.util.ArrayList` ，而是 `java.util.Arrays` 的一个内部类,这个内部类并没有实现集合的修改方法或者说并没有重写这些方法。

```java
List myList = Arrays.asList(1, 2, 3);
myList.add(4);//运行时报错：UnsupportedOperationException
myList.remove(1);//运行时报错：UnsupportedOperationException
myList.clear();//运行时报错：UnsupportedOperationException

System.out.println(myList.getClass());//class java.util.Arrays$ArrayList
```

下图是`java.util.Arrays$ArrayList`的简易源码，我们可以看到这个类重写的方法有哪些。

```java
  private static class ArrayList<E> extends AbstractList<E>
        implements RandomAccess, java.io.Serializable
    {
        ...

        @Override
        public E get(int index) {
          ...
        }

        @Override
        public E set(int index, E element) {
          ...
        }

        @Override
        public int indexOf(Object o) {
          ...
        }

        @Override
        public boolean contains(Object o) {
           ...
        }

        @Override
        public void forEach(Consumer<? super E> action) {
          ...
        }

        @Override
        public void replaceAll(UnaryOperator<E> operator) {
          ...
        }

        @Override
        public void sort(Comparator<? super E> c) {
          ...
        }
    }
```

我们再看一下`java.util.AbstractList`的`remove()`方法，这样我们就明白为啥会抛出`UnsupportedOperationException`。

```java
public E remove(int index) {
    throw new UnsupportedOperationException();
}
```

4、如何正确的将数组转换为ArrayList?

stackoverflow：https://dwz.cn/vcBkTiTW

- 自己动手实现（教育目的）


```java
//JDK1.5+
static <T> List<T> arrayToList(final T[] array) {
  final List<T> l = new ArrayList<T>(array.length);

  for (final T s : array) {
    l.add(s);
  }
  return (l);
}
```

```java
Integer [] myArray = { 1, 2, 3 };
System.out.println(arrayToList(myArray).getClass());//class java.util.ArrayList
```

- 最简便的方法(推荐)


```java
List list = new ArrayList<>(Arrays.asList("a", "b", "c"))
```

- 使用 Java8 的Stream(推荐)


```java
Integer [] myArray = { 1, 2, 3 };
List myList = Arrays.stream(myArray).collect(Collectors.toList());
//基本类型也可以实现转换（依赖boxed的装箱操作）
int [] myArray2 = { 1, 2, 3 };
List myList = Arrays.stream(myArray2).boxed().collect(Collectors.toList());
```

- 使用 Guava(推荐)
  - 对于不可变集合，你可以使用[`ImmutableList`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/ImmutableList.java)类及其[`of()`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/ImmutableList.java#L101)与[`copyOf()`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/ImmutableList.java#L225)工厂方法：（参数不能为空）
  - 对于可变集合，你可以使用[`Lists`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/Lists.java)类及其[`newArrayList()`](https://github.com/google/guava/blob/master/guava/src/com/google/common/collect/Lists.java#L87)工厂方法：

```java
List<String> il = ImmutableList.of("string", "elements");  // from varargs
List<String> il = ImmutableList.copyOf(aStringArray);      // from array
```
```java
List<String> l1 = Lists.newArrayList(anotherListOrCollection);    // from collection
List<String> l2 = Lists.newArrayList(aStringArray);               // from array
List<String> l3 = Lists.newArrayList("or", "string", "elements"); // from varargs
```

- 使用 Apache Commons Collections


```java
List<String> list = new ArrayList<String>();
CollectionUtils.addAll(list, str);
```

#### 2.3. LinkedList

##### 1. 简介

`LinkedList`是一个实现了`List`接口和`Deque`接口的双端链表。 

- `LinkedList`底层的链表结构使它支持高效的插入和删除操作，另外它实现了`Deque`接口，使得`LinkedList`类也具有队列的特性;
- `LinkedList`不是线程安全的，如果想使`LinkedList`变成线程安全的，可以调用静态类`Collections`类中的`synchronizedList`方法： 

```java
List list=Collections.synchronizedList(new LinkedList(...));
```

##### 2. 内部结构分析

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115092439734.png" alt="image-20210115092439734" style="zoom:67%;" />

看完了图之后，我们再看LinkedList类中的一个内部私有类Node就很好理解了：
```java
private static class Node<E> {
        E item;//节点值
        Node<E> next;//后继节点
        Node<E> prev;//前驱节点

        Node(Node<E> prev, E element, Node<E> next) {
            this.item = element;
            this.next = next;
            this.prev = prev;
        }
    }
```
这个类就代表双端链表的节点Node。这个类有三个属性，分别是前驱节点，本节点的值，后继结点。

>LinkedList双向链表，创建链表的时候不带头节点。first为第一个节点，last为最后一个节点

##### 3. 源码分析

1、构造方法

- 空构造方法：

```java
public LinkedList() {
}
```

- 用已有的集合创建链表的构造方法：

```java
public LinkedList(Collection<? extends E> c) {
    this();
    addAll(c);
}
```
2、add方法

- add(E e) 方法：将元素添加到链表尾部

```java
public boolean add(E e) {
        linkLast(e);//这里就只调用了这一个方法
        return true;
    }
```

```java
/**
 * 链接使e作为最后一个元素。
 */
void linkLast(E e) {
    final Node<E> l = last;
    final Node<E> newNode = new Node<>(l, e, null);
    last = newNode;//新建节点  更新尾节点
    if (l == null)
        first = newNode;
    else
        l.next = newNode;//指向后继元素也就是指向下一个元素
    size++;
    modCount++;
}
```

- add(int index,E e)：在指定位置添加元素


```java
public void add(int index, E element) {
    checkPositionIndex(index); //检查索引是否处于[0-size]之间

    if (index == size)//添加在链表尾部
        linkLast(element);
    else//添加在链表中间
        linkBefore(element, node(index));
}
```
linkBefore方法需要给定两个参数，一个插入节点的值，一个指定的node，所以我们又调用了`node(index)`去找到index对应的node。

- addAll(Collection  c )：将集合插入到链表尾部


```java
public boolean addAll(Collection<? extends E> c) {
    return addAll(size, c);
}
```

- addAll(int index, Collection c)： 将集合从指定位置开始插入


```java
public boolean addAll(int index, Collection<? extends E> c) {
    //1:检查index范围是否在size之内
    checkPositionIndex(index);

    //2:toArray()方法把集合的数据存到对象数组中
    Object[] a = c.toArray();
    int numNew = a.length;
    if (numNew == 0)
        return false;

    //3：得到插入位置的前驱节点和后继节点
    Node<E> pred, succ;
    //如果插入位置为尾部，前驱节点为last，后继节点为null
    if (index == size) {
        succ = null;
        pred = last;
    }
    //否则，调用node()方法得到后继节点，再得到前驱节点
    else {
        succ = node(index);
        pred = succ.prev;
    }

    // 4：遍历数据将数据插入
    for (Object o : a) {
        @SuppressWarnings("unchecked") E e = (E) o;
        //创建新节点
        Node<E> newNode = new Node<>(pred, e, null);
        //如果插入位置在链表头部
        if (pred == null)
            first = newNode;
        else
            pred.next = newNode;
        pred = newNode;  //新节点为前驱节点
    }

    //如果插入位置在尾部，重置last节点
    if (succ == null) {
        last = pred;
    }
    //否则，将插入的链表与先前链表连接起来
    else {
        pred.next = succ;
        succ.prev = pred;
    }

    size += numNew;
    modCount++;
    return true;
}    
```
上面可以看出addAll方法通常包括下面四个步骤：

1. 检查index范围是否在size之内
2. toArray()方法把集合的数据存到对象数组中
3. 得到插入位置的前驱和后继节点
4. 遍历数据，将数据插入到指定位置
5. 更新前驱节点和后继节点，并将链表链接起来

- addFirst(E e)： 将元素添加到链表头部

```java
 public void addFirst(E e) {
        linkFirst(e);
    }
```
```java
private void linkFirst(E e) {
    final Node<E> f = first;
    final Node<E> newNode = new Node<>(null, e, f);//新建节点，以头节点为后继节点
    first = newNode;  //更新头节点
    //如果链表为空，last节点也指向该节点
    if (f == null)
        last = newNode;
    //否则，将头节点的前驱指针指向新节点，也就是指向前一个元素
    else
        f.prev = newNode;
    size++;
    modCount++;
}
```
- addLast(E e)： 将元素添加到链表尾部，与 **add(E e)** 方法一样

```java
public void addLast(E e) {
    linkLast(e);
}
```

3、根据位置取数据的方法

- get(int index)： 根据指定索引返回数据


```java
public E get(int index) {
    //检查index范围是否在size之内
    checkElementIndex(index);
    //调用Node(index)去找到index对应的node然后返回它的值
    return node(index).item;
}
```

```java
Node<E> node(int index) {
	// assert isElementIndex(index);
    //如果索引小于当前队列长度的一半则从前半段头节点first进行遍历
	if (index < (size >> 1)) {
		Node<E> x = first;
		for (int i = 0; i < index; i++)
			x = x.next;
		return x;
	} else {  //如果索引大于当前队列长度的一半则从后半段尾节点last进行遍历
		Node<E> x = last;
		for (int i = size - 1; i > index; i--)
			x = x.prev;
		return x;
	}
}
```

- 获取头节点（index=0）数据方法
  - 区别：getFirst(),element(),peek(),peekFirst()
    - getFirst(),element(),peek(),peekFirst()这四个获取头结点方法的区别在于对链表为空时的处理，是抛出异常还是返回null
    - 其中getFirst() 和element() 方法将会在链表为空时，抛出异常。`element()`方法的内部就是使用`getFirst()`实现的。它们会在链表为空时，抛出`NoSuchElementException  `
    - peek(),peekFirst()方法将会在链表为空时，返回null

```java
public E getFirst() {
    final Node<E> f = first;
    if (f == null)
        throw new NoSuchElementException();
    return f.item;
}
public E element() {
    return getFirst();
}
public E peek() {
    final Node<E> f = first;
    return (f == null) ? null : f.item;
}

public E peekFirst() {
    final Node<E> f = first;
    return (f == null) ? null : f.item;
 }
```
- 
  获取尾节点（index=-1）数据方法:

```java
 public E getLast() {
    final Node<E> l = last;
    if (l == null)
        throw new NoSuchElementException();
    return l.item;
}
public E peekLast() {
    final Node<E> l = last;
    return (l == null) ? null : l.item;
}
```
两者区别：getLast() 方法在链表为空时，会抛出NoSuchElementException，而peekLast() 则不会，只是会返回 null。

4、根据对象得到索引的方法

- int indexOf(Object o)： 从头遍历找

```java
public int indexOf(Object o) {
    int index = 0;
    if (o == null) {
        //从头遍历
        for (Node<E> x = first; x != null; x = x.next) {
            if (x.item == null)
                return index;
            index++;
        }
    } else {
        //从头遍历
        for (Node<E> x = first; x != null; x = x.next) {
            if (o.equals(x.item))
                return index;
            index++;
        }
    }
    return -1;
}
```

- int lastIndexOf(Object o)： 从尾遍历找


```java
public int lastIndexOf(Object o) {
        int index = size;
        if (o == null) {
            //从尾遍历
            for (Node<E> x = last; x != null; x = x.prev) {
                index--;
                if (x.item == null)
                    return index;
            }
        } else {
            //从尾遍历
            for (Node<E> x = last; x != null; x = x.prev) {
                index--;
                if (o.equals(x.item))
                    return index;
            }
        }
        return -1;
    }
```

5、检查链表是否包含某对象的方法：

contains(Object o)： 检查对象o是否存在于链表中
```java
 public boolean contains(Object o) {
    return indexOf(o) != -1;
}
```

6、删除方法

- remove() ,removeFirst(), pop(): 删除头节点


```java
public E pop() {
    return removeFirst();
}
public E remove() {
    return removeFirst();
}
public E removeFirst() {
    final Node<E> f = first;
    if (f == null)
        throw new NoSuchElementException();
    return unlinkFirst(f);
}
```

- removeLast(),pollLast(): 删除尾节点


```java
public E removeLast() {
    final Node<E> l = last;
    if (l == null)
        throw new NoSuchElementException();
    return unlinkLast(l);
}
public E pollLast() {
    final Node<E> l = last;
    return (l == null) ? null : unlinkLast(l);
}
```
区别： removeLast()在链表为空时将抛出NoSuchElementException，而pollLast()方法返回null。

- remove(Object o): 删除指定元素


```java
public boolean remove(Object o) {
        //如果删除对象为null
        if (o == null) {
            //从头开始遍历
            for (Node<E> x = first; x != null; x = x.next) {
                //找到元素
                if (x.item == null) {
                   //从链表中移除找到的元素
                    unlink(x);
                    return true;
                }
            }
        } else {
            //从头开始遍历
            for (Node<E> x = first; x != null; x = x.next) {
                //找到元素
                if (o.equals(x.item)) {
                    //从链表中移除找到的元素
                    unlink(x);
                    return true;
                }
            }
        }
        return false;
    }
```

当删除指定对象时，只需调用remove(Object o)即可，不过该方法一次只会删除一个匹配的对象，如果删除了匹配对象，返回true，否则false。

- unlink(Node<E> x) 方法：

```java
E unlink(Node<E> x) {
    // assert x != null;
    final E element = x.item;
    final Node<E> next = x.next;//得到后继节点
    final Node<E> prev = x.prev;//得到前驱节点

    //删除前驱指针
    if (prev == null) {
        first = next;//如果删除的节点是头节点,令头节点指向该节点的后继节点
    } else {
        prev.next = next;//将前驱节点的后继节点指向后继节点
        x.prev = null;
    }

    //删除后继指针
    if (next == null) {
        last = prev;//如果删除的节点是尾节点,令尾节点指向该节点的前驱节点
    } else {
        next.prev = prev;
        x.next = null;
    }
    x.item = null;
    size--;
    modCount++;
    return element;
}
```

remove(int index)：删除指定位置的元素
```java
public E remove(int index) {
    //检查index范围
    checkElementIndex(index);
    //将节点删除
    return unlink(node(index));
}
```

##### 4. LinkedList类常用方法测试

```java
package list;

import java.util.Iterator;
import java.util.LinkedList;

public class LinkedListDemo {
    public static void main(String[] srgs) {
        //创建存放int类型的linkedList
        LinkedList<Integer> linkedList = new LinkedList<>();
        /************************** linkedList的基本操作 ************************/
        linkedList.addFirst(0); // 添加元素到列表开头
        linkedList.add(1); // 在列表结尾添加元素
        linkedList.add(2, 2); // 在指定位置添加元素
        linkedList.addLast(3); // 添加元素到列表结尾
        
        System.out.println("LinkedList（直接输出的）: " + linkedList);

        System.out.println("getFirst()获得第一个元素: " + linkedList.getFirst()); // 返回此列表的第一个元素
        System.out.println("getLast()获得第最后一个元素: " + linkedList.getLast()); // 返回此列表的最后一个元素
        System.out.println("removeFirst()删除第一个元素并返回: " + linkedList.removeFirst()); // 移除并返回此列表的第一个元素
        System.out.println("removeLast()删除最后一个元素并返回: " + linkedList.removeLast()); // 移除并返回此列表的最后一个元素
        System.out.println("After remove:" + linkedList);
        System.out.println("contains()方法判断列表是否包含1这个元素:" + linkedList.contains(1)); // 判断此列表包含指定元素，如果是，则返回true
        System.out.println("该linkedList的大小 : " + linkedList.size()); // 返回此列表的元素个数

        /************************** 位置访问操作 ************************/
        System.out.println("-----------------------------------------");
        linkedList.set(1, 3); // 将此列表中指定位置的元素替换为指定的元素
        System.out.println("After set(1, 3):" + linkedList);
        System.out.println("get(1)获得指定位置（这里为1）的元素: " + linkedList.get(1)); // 返回此列表中指定位置处的元素

        /************************** Search操作 ************************/
        System.out.println("-----------------------------------------");
        linkedList.add(3);
        System.out.println("indexOf(3): " + linkedList.indexOf(3)); // 返回此列表中首次出现的指定元素的索引
        System.out.println("lastIndexOf(3): " + linkedList.lastIndexOf(3));// 返回此列表中最后出现的指定元素的索引

        /************************** Queue操作 ************************/
        System.out.println("-----------------------------------------");
        System.out.println("peek(): " + linkedList.peek()); // 获取但不移除此列表的头
        System.out.println("element(): " + linkedList.element()); // 获取但不移除此列表的头
        linkedList.poll(); // 获取并移除此列表的头
        System.out.println("After poll():" + linkedList);
        linkedList.remove();
        System.out.println("After remove():" + linkedList); // 获取并移除此列表的头
        linkedList.offer(4);
        System.out.println("After offer(4):" + linkedList); // 将指定元素添加到此列表的末尾

        /************************** Deque操作 ************************/
        System.out.println("-----------------------------------------");
        linkedList.offerFirst(2); // 在此列表的开头插入指定的元素
        System.out.println("After offerFirst(2):" + linkedList);
        linkedList.offerLast(5); // 在此列表末尾插入指定的元素
        System.out.println("After offerLast(5):" + linkedList);
        System.out.println("peekFirst(): " + linkedList.peekFirst()); // 获取但不移除此列表的第一个元素
        System.out.println("peekLast(): " + linkedList.peekLast()); // 获取但不移除此列表的第一个元素
        linkedList.pollFirst(); // 获取并移除此列表的第一个元素
        System.out.println("After pollFirst():" + linkedList);
        linkedList.pollLast(); // 获取并移除此列表的最后一个元素
        System.out.println("After pollLast():" + linkedList);
        linkedList.push(2); // 将元素推入此列表所表示的堆栈（插入到列表的头）
        System.out.println("After push(2):" + linkedList);
        linkedList.pop(); // 从此列表所表示的堆栈处弹出一个元素（获取并移除列表第一个元素）
        System.out.println("After pop():" + linkedList);
        linkedList.add(3);
        linkedList.removeFirstOccurrence(3); // 从此列表中移除第一次出现的指定元素（从头部到尾部遍历列表）
        System.out.println("After removeFirstOccurrence(3):" + linkedList);
        linkedList.removeLastOccurrence(3); // 从此列表中移除最后一次出现的指定元素（从尾部到头部遍历列表）
        System.out.println("After removeFirstOccurrence(3):" + linkedList);

        /************************** 遍历操作 ************************/
        System.out.println("-----------------------------------------");
        linkedList.clear();
        for (int i = 0; i < 100000; i++) {
            linkedList.add(i);
        }
        // 迭代器遍历
        long start = System.currentTimeMillis();
        Iterator<Integer> iterator = linkedList.iterator();
        while (iterator.hasNext()) {
            iterator.next();
        }
        long end = System.currentTimeMillis();
        System.out.println("Iterator：" + (end - start) + " ms");

        // 顺序遍历(随机遍历)
        start = System.currentTimeMillis();
        for (int i = 0; i < linkedList.size(); i++) {
            linkedList.get(i);
        }
        end = System.currentTimeMillis();
        System.out.println("for：" + (end - start) + " ms");

        // 另一种for循环遍历
        start = System.currentTimeMillis();
        for (Integer i : linkedList)
            ;
        end = System.currentTimeMillis();
        System.out.println("for2：" + (end - start) + " ms");

        // 通过pollFirst()或pollLast()来遍历LinkedList
        LinkedList<Integer> temp1 = new LinkedList<>();
        temp1.addAll(linkedList);
        start = System.currentTimeMillis();
        while (temp1.size() != 0) {
            temp1.pollFirst();
        }
        end = System.currentTimeMillis();
        System.out.println("pollFirst()或pollLast()：" + (end - start) + " ms");

        // 通过removeFirst()或removeLast()来遍历LinkedList
        LinkedList<Integer> temp2 = new LinkedList<>();
        temp2.addAll(linkedList);
        start = System.currentTimeMillis();
        while (temp2.size() != 0) {
            temp2.removeFirst();
        }
        end = System.currentTimeMillis();
        System.out.println("removeFirst()或removeLast()：" + (end - start) + " ms");
    }
}
```

### 3. Set

1、无序性和不可重复性的含义是什么

- 什么是无序性？无序性不等于随机性 ，无序性是指存储的数据在底层数组中并非按照数组索引的顺序添加 ，而是根据数据的哈希值决定的。
- 什么是不可重复性？不可重复性是指添加的元素按照 equals()判断时 ，返回 false，需要同时重写 equals()方法和 HashCode()方法。

2、比较 HashSet、LinkedHashSet 和 TreeSet 三者的异同

- `HashSet` 是 Set 接口的主要实现类 ，HashSet 的底层是 HashMap，线程不安全的，可以存储 null 值；
- `LinkedHashSet` 是 HashSet 的子类，默认按照添加的顺序遍历；
- `TreeSet` 底层使用红黑树，默认按照自然排序进行遍历，排序的方式有自然排序和定制排序。

#### 3.1. HashSet

##### 1. HashSet 如何检查重复

当你把对象加入`HashSet`时，HashSet 会先计算对象的`hashcode`值来判断对象加入的位置，同时也会与其他加入的对象的 hashcode 值作比较，如果没有相符的 hashcode，HashSet 会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调用`equals()`方法来检查 hashcode 相等的对象是否真的相同。如果两者相同，HashSet 就不会让加入操作成功。（摘自我的 Java 启蒙书《Head fist java》第二版）

1、hashcode

- 顶级类Object里面的方法，所有的类都是继承Object,返回是一个int类型的数值
    * public native int hashCode();

- 数值生成规则: 根据一定的hash规则(存储地址，字段，长度等)，映射成一个数值，即散列值hashcode

- 可以重写hashcode自定义生成规则。
    * 自定义类中重写hashCode方法，一般使用顶层的Objects.hash方法传入该对象的属性值来生成hasncode，足够散列
        * Objects.hash(age, name, time);
    * 也可以根据业务使用自定义的规则

2、equals

- 顶级类Object里面的方法，所有的类都是继承Object,返回是一个boolean类型
    * public boolean equals(Object obj) { return (this == obj); }
    * 默认比较的是两个对象的内存地址
- 根据自定义的匹配规则，用于匹配两个对象是否一样，一般逻辑如下
    * 首先判断地址是否一样，如果地址一样则直接返回true
    * 非空判断和Class类型判断
        * 如果为空则返回false
        * 如果Class类型不一致则返回false
    * 强转对象
    * 对象里面的属性一一匹配判断
        * 可以使用Objects.equals来进行判断是否相等

3、hashCode()与 equals()的相关规定：

- 如果两个对象相等，则 hashcode 一定也是相同的
- 两个对象相等,对两个 equals 方法返回 true
- 两个对象有相同的 hashcode 值，它们也不一定是相等的
- 综上，equals 方法被覆盖过，则 hashCode 方法也必须被覆盖
- hashCode()的默认行为是对堆上的对象产生独特值。如果没有重写 hashCode()，则该 class 的两个对象无论如何都不会相等（即使这两个对象指向相同的数据）。

4、==与 equals 的区别

- 对于基本类型来说，== 比较的是值是否相等；

- 对于引用类型来说，== 比较的是两个引用是否指向同一个对象地址（两者在内存中存放的地址（堆内存地址）是否指向同一个地方）；

- 对于引用类型（包括包装类型）来说，equals 如果没有被重写，对比它们的地址是否相等；如果 equals()方法被重写（例如 String），则比较的是地址里的内容。



##### 2. 正确使用 equals 方法

Object的equals方法容易抛空指针异常，应使用常量或确定有值的对象来调用 equals

举个例子：
```java
// 不能使用一个值为null的引用类型变量来调用非静态方法，否则会抛出异常
String str = null;
if (str.equals("SnailClimb")) {
  ...
} else {
  ..
}
```

运行上面的程序会抛出空指针异常，但是我们把第二行的条件判断语句改为下面这样的话，就不会抛出空指针异常，else 语句块得到执行。：
```java
"SnailClimb".equals(str);// false
```

不过更推荐使用 java.util.Objects#equals(JDK7 引入的工具类)。
```java
Objects.equals(null,"SnailClimb");// false
```


我们看一下java.util.Objects#equals的源码就知道原因了。
```java
public static boolean equals(Object a, Object b) {
        // 可以避免空指针异常。如果a==null的话此时a.equals(b)就不会得到执行，避免出现空指针异常。
        return (a == b) || (a != null && a.equals(b));
}
```
注意:

* 每种原始类型都有默认值，如int默认值为 0，boolean 的默认值为 false，null 是任何引用类型的默认值，不严格的说是所有 Object 类型的默认值。
* 可以使用 == 或者 != 操作来比较null值，但是不能使用其他算法或者逻辑操作。在Java中`null == null`将返回true。
* 不能使用一个值为null的引用类型变量来调用非静态方法，否则会抛出异常

代码实战: 编写一个User对象，重写里面的hashcode和equal方法

```java
import java.util.Date;
import java.util.Objects;

public class User {
    private int age;
    private  String name;
    private Date time;
    ...
    
	//hashcode一般使用顶层的Objects.hash方法来生成，传入该对象的属性值
    @Override
    public int hashCode() {
        return Objects.hash(age, name, time);
    }

    @Override
    public boolean equals(Object o) {
        //1.首先判断地址是否一样，如果地址一样则直接返回true
        if (this == o) return true;
        //2.非空判断和Class类型判断  2.1 如果为空则返回false  2.2 如果Class类型不一致则返回false
        if (o == null || getClass() != o.getClass()) return false;
        //3.强制转换
        User user = (User) o;
        //对象里面的属性一一匹配判断
        return age == user.age &&
                Objects.equals(name, user.name) &&
                Objects.equals(time, user.time);
    }
}
```

### 4. Map

#### 4.1. Map集合概述

1、`Map`

- `HashMap`： JDK1.8 之前 HashMap 由 **数组+链表** 组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）。JDK1.8 以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将**链表转化为红黑树**，以**减少搜索时间**

- `LinkedHashMap`： `LinkedHashMap` 继承自 `HashMap`，所以它的底层仍然是基于拉链式散列结构即由**数组和链表或红黑树**组成。另外，`LinkedHashMap` 在上面结构的基础上，增加了一条**双向链表**，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。

- `Hashtable`： **数组+链表** 组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的

- `TreeMap`： **红黑树**（自平衡的排序二叉树）

2、HashMap 和 Hashtable 的区别

1. 线程是否安全： `HashMap` 是非线程安全的，`Hashtable` 是线程安全的,因为 `Hashtable` 内部的方法基本都经过`synchronized` 修饰。（如果你要保证线程安全的话就使用 ConcurrentHashMap 吧！）；
2. 效率： 因为线程安全的问题，`HashMap` 要比 `Hashtable` 效率高一点。另外，Hashtable 基本被淘汰，不要在代码中使用它；
3. 对 Null key 和 Null value 的支持： `HashMap` 可以存储 null 的 key 和 value，但 null 作为键只能有一个，null 作为值可以有多个；`Hashtable` 不允许有 null 键和 null 值，否则会抛出 `NullPointerException`。
4. 初始容量大小和每次扩充容量大小的不同 ： ① 创建时如果不指定容量初始值，`Hashtable` 默认的初始大小为 11，之后每次扩充，容量变为原来的 `2n+1`。`HashMap` 默认的初始化大小为 16。之后每次扩充，容量变为原来的 2 倍。② 创建时如果给定了容量初始值，那么 `Hashtable` 会直接使用你给定的大小，而 `HashMap` 会将其扩充为 2 的幂次方大小（`HashMap` 中的`tableSizeFor()`方法保证，下面给出了源代码）。也就是说 HashMap 总是使用 2 的幂作为哈希表的大小,后面会介绍到为什么是 2 的幂次方。
5. 底层数据结构： JDK1.8 以后的 `HashMap` 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。`Hashtable` 没有这样的机制，底层使用数组+链表。

3、部分源码


HashMap部分源码
```java
public class HashMap<K,V> ...{
    //默认容量为16 。不是直接写成16而是使用位运算1<<4  计算机可以直接执行位运算而不需要转换
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4; // aka 16 1*2^4
    
    //默认加载因子
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
    ...
    public HashMap() {
        this.loadFactor = DEFAULT_LOAD_FACTOR; // all other fields defaulted
    }
    //修改操作没有加锁，非线程安全
    public V put(K key, V value) {
	    return putVal(hash(key), key, value, false, true);
    }
    final V putVal(int hash, K key, V value, boolean onlyIfAbsent,boolean evict) {
	    ...
    }
｝
```

Hashtable部分源码
```java
public class Hashtable<K,V> ...{
	public Hashtable() {
        //初始容量为11
        this(11, 0.75f);
    }
    //使用了synchronized进行加锁，线程安全
    public synchronized V put(K key, V value) {
	    ...
    }
｝
```

HashMap 中带有初始容量的构造函数：

```java
    public HashMap(int initialCapacity, float loadFactor) {
        if (initialCapacity < 0)
            throw new IllegalArgumentException("Illegal initial capacity: " +
                                               initialCapacity);
        if (initialCapacity > MAXIMUM_CAPACITY)
            initialCapacity = MAXIMUM_CAPACITY;
        if (loadFactor <= 0 || Float.isNaN(loadFactor))
            throw new IllegalArgumentException("Illegal load factor: " +
                                               loadFactor);
        this.loadFactor = loadFactor;
        this.threshold = tableSizeFor(initialCapacity);
    }
     public HashMap(int initialCapacity) {
        this(initialCapacity, DEFAULT_LOAD_FACTOR);
    }
```

>`tableSizeFor`返回一个大于或等于`cap`容量的最小的2的n次幂的数。`tableSizeFor`以及扩容时为原先容量的2倍这两个步骤保证了 HashMap 总是使用 2 的幂作为哈希表的大小

```java
/**
 * Returns a power of two size for the given target capacity. 
 */
static final int tableSizeFor(int cap) {
    int n = cap - 1;
    n |= n >>> 1;
    n |= n >>> 2;
    n |= n >>> 4;
    n |= n >>> 8;
    n |= n >>> 16;
    return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
}
```

tableSizeFor算法分析
假设n对应的二进制表示为01xxx...xxxx

```
n为01xxx...xxxx
对n右移1位：001xx...xxx，再与n本身位或：011xx...xxx。
对n右移2为：00011...xxx，再位或：01111...xxx，此时前面已经有四个1
对n右移4位再位或：可得8个1.
对n右移8位再位或：可得16个1.
对n右移16位再位或：可得32个1.  
int类型4个字节，最大为32位
```
综上可得，该算法通过几次无符号右移和|操作,会让最高位的1后面(右面)的位全变为1,最后再让结果`n+1`，二进制向前进数，最终得到了2的整数次幂的值

如果n为负数，最高位为1，执行完上面的几次无符号右移和|操作,最高位的1后面的位全变为1(11111111 11111111 11111111 11111111)。最终结果n都为-1。此时该方法返回0。

`int n = cap - 1;`  使用位、或运算之前减1是必要的，确保最终的2的整数次幂的值大于或等于`cap`。如果cap需要的容量正好是2的整数次幂，例如8，则返回的扩容数为8。如果不执行减1操作则返回的扩容数为16。

```
例如cap为8，二进制1000，如果不对它减1而直接操作，将得到答案10000，即16。显然不是结果。减1后二进制为111，再进行后续操作则会得到原来的数值1000，即8。
```

4、HashMap 和 HashSet 区别

如果你看过 `HashSet` 源码的话就应该知道：`HashSet` 底层就是基于 `HashMap` 实现的。（`HashSet` 的源码非常非常少，因为除了 `clone()`、`writeObject()`、`readObject()`是 `HashSet` 自己不得不实现之外，其他方法都是直接调用 `HashMap` 中的方法。

| HashMap                            | HashSet                                                      |
| :--------------------------------- | ------------------------------------------------------------ |
| 实现了 Map 接口                    | 实现 Set 接口                                                |
| 存储键值对                         | 仅存储对象                                                   |
| 调用 `put()`向 map 中添加元素      | 调用 `add()`方法向 Set 中添加元素                            |
| HashMap 使用键（Key）计算 Hashcode | HashSet 使用成员对象来计算 hashcode 值，对于两个对象来说 hashcode 可能相同，所以 equals()方法用来判断对象的相等性， |

5、Set和Map的关系

* set核心就是不保存重复的元素，存储一组唯一的对象

* set的每一种实现都是对应Map里面的一种封装，即set的具体实现其实是map。利用了map里面的一些规则来实现。
    * HashSet对应的就是HashMap，treeSet对应的就是treeMap

```java
//HashSet
public HashSet() {
	map = new HashMap<>();
}
public boolean add(E e) {
	return map.put(e, PRESENT)==null;
}
//TreeSet
public TreeSet() {
	this(new TreeMap<E,Object>());
}
public boolean add(E e) {
	return m.put(e, PRESENT)==null;
}
```

6、HashMap 和 LinkedHashMap 区别


LinkedHashMap 继承自 HashMap，在 HashMap 基础上，通过维护一条**双向链表**，解决了 HashMap 不能随时保持遍历顺序和插入顺序一致的问题。除此之外，LinkedHashMap 对访问顺序也提供了相关支持。在一些场景下，该特性很有用，比如缓存。在实现上，LinkedHashMap 很多方法直接继承自 HashMap，仅为维护双向链表覆写了部分方法

LinkedHashMap遍历顺序是按照**插入顺序**进行遍历的

7、HashMap 和 TreeMap 区别

`TreeMap` 和`HashMap` 都继承自`AbstractMap` ，但是需要注意的是`TreeMap`它还实现了`NavigableMap`接口和`SortedMap` 接口。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115101454246.png" alt="image-20210115101454246" style="zoom:50%;" />

* 实现 `NavigableMap` 接口让 `TreeMap` 有了对集合内元素的搜索的能力。

* 实现`SortMap`接口让 `TreeMap` 有了对集合中的元素根据键排序的能力。默认是按 key 的升序排序，不过我们也可以指定排序的比较器来自定义排序规则，需要实现Comparator接口。
    * 能便捷的实现内部元素的各种排序，但是一般性能比HashMap差，适用于自然排序(按照key的字典顺序来排序(升序))或者自定义排序规则

* TreeMap存储结构：使用存储结构是一个平衡二叉树->红黑树

 排序示例代码如下：
```java
/**
 * @author shuang.kou
 * @createTime 2020年06月15日 17:02:00
 */
public class Person {
    private Integer age;

    public Person(Integer age) {
        this.age = age;
    }

    public Integer getAge() {
        return age;
    }
    public static void main(String[] args) {
        TreeMap<Person, String> treeMap = new TreeMap<>(new Comparator<Person>() {
            @Override
            public int compare(Person person1, Person person2) {
                int num = person1.getAge() - person2.getAge();
                return Integer.compare(num, 0);  //第一个小于第二个 从小到大
            }
        });
        treeMap.put(new Person(3), "person1");
        treeMap.put(new Person(18), "person2");
        treeMap.put(new Person(35), "person3");
        treeMap.put(new Person(16), "person4");
        treeMap.entrySet().stream().forEach(personStringEntry -> {
            System.out.println(personStringEntry.getValue());
        });
    }
}
```

输出:

```
person1
person4
person2
person3
```

可以看出，`TreeMap` 中的元素已经是按照 `Person` 的 age 字段的升序来排列了。

上面，我们是通过传入匿名内部类的方式实现的，你可以将代码替换成 Lambda 表达式实现的方式：

```java
TreeMap<Person, String> treeMap = new TreeMap<>((person1, person2) -> {
  int num = person1.getAge() - person2.getAge();
  return Integer.compare(num, 0);
});
```

综上，相比于`HashMap`来说 `TreeMap` 主要多了对集合中的元素根据键排序的能力以及对集合内元素的搜索的能力。

8、TreeMap使用场景

常见Map的排序规则

* 按照添加时顺序使用LinkedHashMap
* 按照自然排序使用TreeMap
* 自定义排序，也是使用TreeMap。创建对象时指定排序规则：TreeMap(Comparetor c)。
  

写过微信支付签名工具类就用这个类

```java
//可以指定排序规则，默认是按照key的字典顺序来排序(升序)
public TreeMap(SortedMap<K, ? extends V> m) {
	comparator = m.comparator();
	try {
		buildFromSorted(m.size(), m.entrySet().iterator(), null, null);
	} catch (java.io.IOException cannotHappen) {
	} catch (ClassNotFoundException cannotHappen) {
	}
}
```

#### 4.2. HashMap

HashMap 主要用来存放键值对，它基于哈希表的Map接口实现，是常用的Java集合之一。 

- JDK1.8 之前 HashMap 由 数组+链表 组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）.
- JDK1.8 以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）时，将链表转化为红黑树（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树），以减少搜索时间，具体可以参考 `treeifyBin`方法。


##### 1. 底层数据结构分析

1、JDK1.8之前

JDK1.8 之前 HashMap 底层是 数组和链表 结合在一起使用也就是 链表散列。HashMap 通过 key 的 hashCode 经过扰动函数处理过后得到 hash  值，然后通过 `(n - 1) & hash` 判断当前元素存放的位置（这里的 n 指的是数组的长度），如果当前位置存在元素的话，就判断该元素与要存入的元素的 hash 值以及 key 是否相同，如果相同的话，直接覆盖，不相同就通过拉链法解决冲突。

- 所谓扰动函数指的就是 HashMap 的 hash 方法。使用 hash 方法也就是扰动函数是为了防止一些实现比较差的 hashCode() 方法 换句话说使用扰动函数之后可以减少碰撞。

- 所谓 “拉链法” 就是：将链表和数组相结合。也就是说创建一个链表数组，数组中每一格就是一个链表。若遇到哈希冲突，则将冲突的值加到链表中即可。
  <img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115105146050.png" alt="image-20210115105146050" style="zoom:50%;" />

什么是Hash碰撞？常见的解决办法有哪些，HashMap采用哪种方法

- hash碰撞的意思是不同key计算得到的Hash值相同，需要放到同个bucket中常见的解决办法 
  - 链表法 HashMap采用的是链表法 放入对象的key的hash值如果和数组中已存在的对象的key的hash值一样，则将该对象放到数组中的entry对象所在的链表中
  - 开发地址法
  - 再哈希法

2、JDK 1.8 HashMap 的 hash 方法源码

- JDK 1.8 的 hash方法 相比于 JDK 1.7 hash 方法更加简化，但是原理不变。


```java
      static final int hash(Object key) {
        int h;
        // key.hashCode()：返回散列值也就是hashcode
        // ^ ：按位异或
        // >>>:无符号右移，忽略符号位，空位都以0补齐
        return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
    }
```

- 对比一下 JDK1.7的 HashMap 的 hash 方法源码.


```java
static int hash(int h) {
    // This function ensures that hashCodes that differ only by
    // constant multiples at each bit position have a bounded
    // number of collisions (approximately 8 at default load factor).

    h ^= (h >>> 20) ^ (h >>> 12);
    return h ^ (h >>> 7) ^ (h >>> 4);
}
```

相比于 JDK1.8 的 hash 方法 ，JDK 1.7 的 hash 方法的性能会稍差一点点，因为毕竟扰动了 4 次。

3、底层存储结构：数组+链表(拉链法)

**“拉链法”** 就是：将链表和数组相结合。也就是说创建一个数组，数组中每一个元素表示hash值对应的一个链表。若遇到哈希冲突，则将冲突的值加到链表中。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115153328325.png" alt="image-20210115153328325" style="zoom:50%;" />

- 数组：`transient Node<K,V>[] table;` `table`为数组, 数组中的元素类型为`Node`，实现了`Map.Entry<K,V>`。数组中的每个node元素对象表示了该哈希值对应单项链表的第一个节点，指向下一个节点。
- 链表：每个数组node对象->next(Node对象)->next-> ... 每个链表存储的是hash值一样但是key不一样的对象

**Node结构:**

```java
static class Node<K,V> implements Map.Entry<K,V> {
	final int hash;
	final K key;
	V value;
	Node<K,V> next;

	Node(int hash, K key, V value, Node<K,V> next) {
		this.hash = hash;
		this.key = key;
		this.value = value;
		this.next = next;
	}
	...
}
```

当添加元素的时候，首先计算key的哈希值，然后通过 `(n - 1) & hash` 判断当前元素应该存放到数组的位置（这里的 n 指的是数组的长度）。如果当前数组的位置没有元素，则创建Node对象（创建对象的时候指定hash,key,value，next为null），并将该Node对象存放到数组对应的位置。

`(n - 1) & hash`  如果哈希值一样，则对应到数组中元素锁表示的一个链表。

**代码如下：**
```java
Node<K,V>[] tab; Node<K,V> p; int n, i;
if ((tab = table) == null || (n = tab.length) == 0)  //tab = table 将数组对象赋值给tab
    n = (tab = resize()).length;
if ((p = tab[i = (n - 1) & hash]) == null)
    tab[i] = newNode(hash, key, value, null);
```

如果当前数组的位置上有元素，判断该元素与要存入的元素的 hash 值以及 key 是否相同，如果相同的话，将该元素赋值给`e`。

**代码如下：**
```java
Node<K,V> e; K k;
if (p.hash == hash &&
	((k = p.key) == key || (key != null && key.equals(k))))
	e = p;
```

不相同就遍历单项链表，挨个比较链表中的每个Node元素与要存入的元素的 hash 值以及 key 是否相同, 如果相同将找到的元素赋值给`e`并跳出遍历，如果一直找到最后一个节点(最后一个节点的下一个节点next为空)仍然没有相同的元素，然后将要存入元素添加到最后一个节点的下一个节点。

**代码如下：**
```java
for (int binCount = 0; ; ++binCount) {
    if ((e = p.next) == null) {
        p.next = newNode(hash, key, value, null);
        if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
            treeifyBin(tab, hash);  
        break;
    }
    if (e.hash == hash &&
        ((k = e.key) == key || (key != null && key.equals(k))))
        break;
    p = e;
}
```

如果有元素与新加入的元素的 hash 值以及 key 相同,则修改已有元素的value值为要新加入元素的value。

 **代码如下：**
```java
if (e != null) { // existing mapping for key
	V oldValue = e.value;
	if (!onlyIfAbsent || oldValue == null)
		e.value = value;
	afterNodeAccess(e);
	return oldValue;
}
```

在JDK1.8中，链表的长度大于8，链表会转换成红黑树。JDK8使用红黑树来替代超过8个节点的链表，主要是查询性能的提升，从原来的O(n)到O(logn)。

通过hash碰撞，让HashMap不断产生碰撞，那么相同的key的位置的链表就会不断增长，当对这个Hashmap的相应位置进行查询的时候，就会循环遍历这个超级大的链表，性能就会下降，所以改用红黑树。
* 链表查询,挨个从头节点进行遍历。时间复杂度为O(n)
* 红黑树查询时间复杂度为O(logn)

**代码如下：**
```java
static final int TREEIFY_THRESHOLD = 8;
...
if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
            treeifyBin(tab, hash);  
```



2、JDK1.8之后

相比于之前的版本， JDK1.8 之后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115153927791.png" alt="image-20210115153927791" style="zoom: 50%;" />

TreeMap、TreeSet 以及 JDK1.8 之后的 HashMap 底层都用到了红黑树。红黑树就是为了解决二叉查找树的缺陷，因为二叉查找树在某些情况下会退化成一个线性结构。

##### 2. HashMap 的长度为什么是 2 的幂次方

HashMap 的长度为什么是 2 的幂次方?

1、加快哈希计算

Hash 值的范围值-2147483648 到 2147483647，前后加起来大概 40 亿的映射空间，只要哈希函数映射得比较均匀松散，一般应用是很难出现碰撞的。但问题是一个 40 亿长度的数组，内存是放不下的。所以这个散列值是不能直接拿来用的。用之前还要先做对数组的长度取模运算，得到的余数才能用来要存放的位置也就是对应的数组下标。这个数组下标的计算方法是“ `(n - 1) & hash`”。（n 代表数组长度）。

>我们首先可能会想到采用%取模的操作来实现即`hash%length`。由于计算机中采用二进制位操作 &，相对于%能够提高运算效率，于是源码中做了优化`hash&(length-1)`，但是`hash%length==hash&(length-1)` ? 重点来了：“取模(%)操作中如果除数是 2 的幂次则等价于与其除数减一的与(&)操作（也就是说 hash%length==hash&(length-1)的前提是 length 必须是 2 的 n 次方；）。” 所以HashMap 的长度是 2 的幂次方此时`hash%length==hash&(length-1)` 

2、减少哈希碰撞(把数据分配均匀)

假设现在数组的长度 n 可能是偶数也可能是奇数。

* n 为偶数时，n-1 为奇数，奇数的二进制最后一位是 1，这样便保证了 `(n - 1) & hash`  的最后一位可能为 0，也可能为 1（这取决于 h 的值），即 & 运算后的结果可能为偶数，也可能为奇数，这样便可以保证散列的均匀性。
```
例如 length = 4，length - 1 = 3, 3 的 二进制是 11
若此时的 hash 是 2，也就是 10，那么 10 & 11 = 10（偶数位置）
hash = 3，即 11 & 11 = 11 （奇数位置）
```

* 如果 n 为奇数的话，很明显 n-1 为偶数，它的最后一位是 0，这样 `(n - 1) & hash`  的最后一位肯定为 0，即只能为偶数，这样任何 hash 值都只会被散列到数组的偶数下标位置上，这便浪费了近一半的空间
```
length = 3， 3 - 1 = 2，他的二进制是 10
10 无论与什么树进行 & 运算，结果都是偶数
```

因此，数组长度n取2的整数次幂，在计算存储数组下标位置时`n-1`,并与哈希值进行与运算`(n - 1) & hash` 。是为了使不同 hash 值发生碰撞的概率较小，这样就能使元素在哈希表中均匀地散列。

##### 3. 类的属性

```java
public class HashMap<K,V> extends AbstractMap<K,V> implements Map<K,V>, Cloneable, Serializable {
    // 序列号
    private static final long serialVersionUID = 362498820763181265L;    
    // 默认的初始容量是16
    static final int DEFAULT_INITIAL_CAPACITY = 1 << 4;   
    // 最大容量
    static final int MAXIMUM_CAPACITY = 1 << 30; 
    // 默认的填充因子
    static final float DEFAULT_LOAD_FACTOR = 0.75f;
    // 当桶(bucket)上的结点数大于这个值时会转成红黑树
    static final int TREEIFY_THRESHOLD = 8; 
    // 当桶(bucket)上的结点数小于这个值时树转链表
    static final int UNTREEIFY_THRESHOLD = 6;
    // 桶中结构转化为红黑树对应的table的最小大小
    static final int MIN_TREEIFY_CAPACITY = 64;
    // 存储元素的数组，总是2的幂次倍
    transient Node<k,v>[] table; 
    // 存放具体元素的集
    transient Set<map.entry<k,v>> entrySet;
    // 存放元素的个数，注意这个不等于数组的长度。
    transient int size;
    // 每次扩容和更改map结构的计数器
    transient int modCount;   
    // 临界值 当实际大小(容量*填充因子)超过临界值时，会进行扩容
    int threshold;
    // 加载因子
    final float loadFactor;
}
```
1、loadFactor加载因子

loadFactor加载因子是控制数组存放数据的疏密程度，loadFactor越趋近于1，那么   数组中存放的数据(entry)也就越多，也就越密，也就是会让链表的长度增加，loadFactor越小，也就是趋近于0，数组中存放的数据(entry)也就越少，也就越稀疏。

loadFactor太大导致查找元素效率低，太小导致数组的利用率低，存放的数据会很分散。loadFactor的默认值为0.75f是官方给出的一个比较好的临界值

给定的默认容量为 16，负载因子为 0.75。Map 在使用过程中不断的往里面存放数据，当数量达到了 16 * 0.75 = 12 就需要将当前 16 的容量进行扩容，而扩容这个过程涉及到 rehash、复制数据等操作，所以非常消耗性能。

2、threshold

threshold表示HashMap中存储元素的临界值。 threshold = capacity * loadFactor，当size>threshold的时候，那么就要考虑对数组的扩增了，也就是说，这个的意思就是 衡量数组是否需要扩增的一个标准。

>容量`capacity`是指HashMap的`table`数组长度。而`threshold` 为数组里面存储元素个数的临界值。`size`为整个hashMap中的元素个数(数组+链表)


Node节点类源码:

```java
// 继承自 Map.Entry<K,V>
static class Node<K,V> implements Map.Entry<K,V> {
       final int hash;// 哈希值，存放元素到hashmap中时用来与其他元素hash值比较
       final K key;//键
       V value;//值
       // 指向下一个节点
       Node<K,V> next;
       Node(int hash, K key, V value, Node<K,V> next) {
            this.hash = hash;
            this.key = key;
            this.value = value;
            this.next = next;
        }
        public final K getKey()        { return key; }
        public final V getValue()      { return value; }
        public final String toString() { return key + "=" + value; }
        // 重写hashCode()方法
        public final int hashCode() {
            return Objects.hashCode(key) ^ Objects.hashCode(value);
        }

        public final V setValue(V newValue) {
            V oldValue = value;
            value = newValue;
            return oldValue;
        }
        // 重写 equals() 方法
        public final boolean equals(Object o) {
            if (o == this)
                return true;
            if (o instanceof Map.Entry) {
                Map.Entry<?,?> e = (Map.Entry<?,?>)o;
                if (Objects.equals(key, e.getKey()) &&
                    Objects.equals(value, e.getValue()))
                    return true;
            }
            return false;
        }
}
```
树节点类源码:
```java
static final class TreeNode<K,V> extends LinkedHashMap.Entry<K,V> {
        TreeNode<K,V> parent;  // 父
        TreeNode<K,V> left;    // 左
        TreeNode<K,V> right;   // 右
        TreeNode<K,V> prev;    // needed to unlink next upon deletion
        boolean red;           // 判断颜色
        TreeNode(int hash, K key, V val, Node<K,V> next) {
            super(hash, key, val, next);
        }
        // 返回根节点
        final TreeNode<K,V> root() {
            for (TreeNode<K,V> r = this, p;;) {
                if ((p = r.parent) == null)
                    return r;
                r = p;
       }
```

##### 4. HashMap源码分析

1、 构造方法

HashMap 中有四个构造方法，它们分别如下：

```java
    // 默认构造函数。
    public HashMap() {
        this.loadFactor = DEFAULT_LOAD_FACTOR; // all   other fields defaulted
     }
     
     // 包含另一个“Map”的构造函数
     public HashMap(Map<? extends K, ? extends V> m) {
         this.loadFactor = DEFAULT_LOAD_FACTOR;
         putMapEntries(m, false);//下面会分析到这个方法
     }
     
     // 指定“容量大小”的构造函数
     public HashMap(int initialCapacity) {
         this(initialCapacity, DEFAULT_LOAD_FACTOR);
     }
     
     // 指定“容量大小”和“加载因子”的构造函数
     public HashMap(int initialCapacity, float loadFactor) {
         if (initialCapacity < 0)
             throw new IllegalArgumentException("Illegal initial capacity: " + initialCapacity);
         if (initialCapacity > MAXIMUM_CAPACITY)
             initialCapacity = MAXIMUM_CAPACITY;
         if (loadFactor <= 0 || Float.isNaN(loadFactor))
             throw new IllegalArgumentException("Illegal load factor: " + loadFactor);
         this.loadFactor = loadFactor;
         this.threshold = tableSizeFor(initialCapacity);
     }
```

```java
/**
 * Returns a power of two size for the given target capacity. 
 */
static final int tableSizeFor(int cap) {
    int n = cap - 1;
    n |= n >>> 1;
    n |= n >>> 2;
    n |= n >>> 4;
    n |= n >>> 8;
    n |= n >>> 16;
    return (n < 0) ? 1 : (n >= MAXIMUM_CAPACITY) ? MAXIMUM_CAPACITY : n + 1;
}
```

putMapEntries方法：

```java
final void putMapEntries(Map<? extends K, ? extends V> m, boolean evict) {
    int s = m.size();
    if (s > 0) {
        // 判断table是否已经初始化
        if (table == null) { // pre-size
            // 未初始化，s为m的实际元素个数
            float ft = ((float)s / loadFactor) + 1.0F;
            int t = ((ft < (float)MAXIMUM_CAPACITY) ?
                    (int)ft : MAXIMUM_CAPACITY);
            // 计算得到的t大于阈值，则初始化阈值
            if (t > threshold)
                threshold = tableSizeFor(t);
        }
        // 已初始化，并且m元素个数大于阈值，进行扩容处理
        else if (s > threshold)
            resize();
        // 将m中的所有元素添加至HashMap中
        for (Map.Entry<? extends K, ? extends V> e : m.entrySet()) {
            K key = e.getKey();
            V value = e.getValue();
            putVal(hash(key), key, value, false, evict);
        }
    }
}
```
2、put方法

HashMap只提供了put用于添加元素，putVal方法只是给put方法调用的一个方法，并没有提供给用户使用。

对putVal方法添加元素的分析如下：

- ①如果定位到的数组位置没有元素 就直接插入数组。
- ②如果定位到的数组位置有元素就和要插入的key比较，如果key相同就直接覆盖，如果key不相同，就判断p是否是一个树节点，如果是就调用`e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value)`将元素添加进入。如果不是就遍历链表插入(插入的是链表尾部)。

ps:下图有一个小问题，来自 [issue#608](https://github.com/Snailclimb/JavaGuide/issues/608)指出：直接覆盖之后应该就会 return，不会有后续操作。参考 JDK8 HashMap.java 658 行。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115105459691.png" alt="image-20210115105459691" style="zoom:70%;" />



```java
public V put(K key, V value) {
    return putVal(hash(key), key, value, false, true);
}

final V putVal(int hash, K key, V value, boolean onlyIfAbsent,
                   boolean evict) {
    Node<K,V>[] tab; Node<K,V> p; int n, i;
    // table未初始化或者长度为0，进行扩容
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;
    // (n - 1) & hash 确定元素存放在哪个桶中，桶为空，新生成结点放入桶中(此时，这个结点是放在数组中)
    if ((p = tab[i = (n - 1) & hash]) == null)
        tab[i] = newNode(hash, key, value, null);
    // 桶中已经存在元素
    else {
        Node<K,V> e; K k;
        // 比较桶中第一个元素(数组中的结点)的hash值相等，key相等
        if (p.hash == hash &&
            ((k = p.key) == key || (key != null && key.equals(k))))
                // 将第一个元素赋值给e，用e来记录
                e = p;
        // hash值不相等，即key不相等；为红黑树结点
        else if (p instanceof TreeNode)
            // 放入树中
            e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
        // 为链表结点
        else {
            // 在链表最末插入结点
            for (int binCount = 0; ; ++binCount) {
                // 到达链表的尾部
                if ((e = p.next) == null) {
                    // 在尾部插入新结点
                    p.next = newNode(hash, key, value, null);
                    // 结点数量达到阈值，转化为红黑树
                    if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                        treeifyBin(tab, hash);
                    // 跳出循环
                    break;
                }
                // 判断链表中结点的key值与插入的元素的key值是否相等
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    // 相等，跳出循环
                    break;
                // 用于遍历桶中的链表，与前面的e = p.next组合，可以遍历链表
                p = e;
            }
        }
        // 表示在桶中找到key值、hash值与插入元素相等的结点
        if (e != null) { 
            // 记录e的value
            V oldValue = e.value;
            // onlyIfAbsent为false或者旧值为null
            if (!onlyIfAbsent || oldValue == null)
                //用新值替换旧值
                e.value = value;
            // 访问后回调
            afterNodeAccess(e);
            // 返回旧值
            return oldValue;
        }
    }
    // 结构性修改
    ++modCount;
    // 实际大小大于阈值则扩容
    if (++size > threshold)
        resize();
    // 插入后回调
    afterNodeInsertion(evict);
    return null;
} 
```

我们再来对比一下 JDK1.7 put方法的代码

对于put方法的分析如下：

- ①如果定位到的数组位置没有元素 就直接插入。
- ②如果定位到的数组位置有元素，遍历以这个元素为头结点的链表，依次和插入的key比较，如果key相同就直接覆盖，不同就采用头插法插入元素。

>不管是头插法还是尾插法都需要先遍历链表查找元素。

```java
public V put(K key, V value)
    if (table == EMPTY_TABLE) { 
    inflateTable(threshold); 
}  
    if (key == null)
        return putForNullKey(value);
    int hash = hash(key);
    int i = indexFor(hash, table.length);
    for (Entry<K,V> e = table[i]; e != null; e = e.next) { // 先遍历
        Object k;
        if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
            V oldValue = e.value;
            e.value = value;
            e.recordAccess(this);
            return oldValue; 
        }
    }

    modCount++;
    addEntry(hash, key, value, i);  // 再插入
    return null;
}
```

3、get方法

```java
public V get(Object key) {
    Node<K,V> e;
    return (e = getNode(hash(key), key)) == null ? null : e.value;
}

final Node<K,V> getNode(int hash, Object key) {
    Node<K,V>[] tab; Node<K,V> first, e; int n; K k;
    if ((tab = table) != null && (n = tab.length) > 0 &&
        (first = tab[(n - 1) & hash]) != null) {
        // 数组元素相等
        if (first.hash == hash && // always check first node
            ((k = first.key) == key || (key != null && key.equals(k))))
            return first;
        // 桶中不止一个节点
        if ((e = first.next) != null) {
            // 在树中get
            if (first instanceof TreeNode)
                return ((TreeNode<K,V>)first).getTreeNode(hash, key);
            // 在链表中get
            do {
                if (e.hash == hash &&
                    ((k = e.key) == key || (key != null && key.equals(k))))
                    return e;
            } while ((e = e.next) != null);
        }
    }
    return null;
}
```
4、resize方法与扩容

```java
if (++size > threshold)
	resize();
```
当元素个数大于`threshold`时才进行扩容

进行扩容，会伴随着一次重新hash分配(rehash)，会遍历hash表中所有的元素进行hash分配，是非常耗时的。在编写程序中，要尽量避免resize。

>resize伴随着rehash

```java
// 默认的初始容量是16
static final int DEFAULT_INITIAL_CAPACITY = 1 << 4;  

static final float DEFAULT_LOAD_FACTOR = 0.75f;

// 加载因子 无参构造不指定默认为DEFAULT_LOAD_FACTOR
final float loadFactor;

// 临界值 当实际大小(容量*填充因子)超过临界值时，会进行扩容
int threshold;

//put操作
final V putVal(int hash, K key, V value, boolean onlyIfAbsent, boolean evict) {
    ...
    // table未初始化或者长度为0，进行扩容
    if ((tab = table) == null || (n = tab.length) == 0)
        n = (tab = resize()).length;
   ...
}
```


```java
final Node<K,V>[] resize() {
    Node<K,V>[] oldTab = table;
    int oldCap = (oldTab == null) ? 0 : oldTab.length;
    int oldThr = threshold;
    int newCap, newThr = 0;
    if (oldCap > 0) {
        // 超过最大值就不再扩充了，就只好随你碰撞去吧
        if (oldCap >= MAXIMUM_CAPACITY) {
            threshold = Integer.MAX_VALUE;
            return oldTab;
        }
        // 没超过最大值，就扩充为原来的2倍
        else if ((newCap = oldCap << 1) < MAXIMUM_CAPACITY && oldCap >= DEFAULT_INITIAL_CAPACITY)
            newThr = oldThr << 1; // double threshold
    }
    else if (oldThr > 0) // initial capacity was placed in threshold
        newCap = oldThr;
    else { 
        // signifies using defaults
        newCap = DEFAULT_INITIAL_CAPACITY;
        newThr = (int)(DEFAULT_LOAD_FACTOR * DEFAULT_INITIAL_CAPACITY);
    }
    // 计算新的resize上限
    if (newThr == 0) {
        float ft = (float)newCap * loadFactor;
        newThr = (newCap < MAXIMUM_CAPACITY && ft < (float)MAXIMUM_CAPACITY ? (int)ft : Integer.MAX_VALUE);
    }
    threshold = newThr;
    @SuppressWarnings({"rawtypes","unchecked"})
        Node<K,V>[] newTab = (Node<K,V>[])new Node[newCap];
    table = newTab;
    if (oldTab != null) {
        // 把每个bucket都移动到新的buckets中
        for (int j = 0; j < oldCap; ++j) {
            Node<K,V> e;
            if ((e = oldTab[j]) != null) {
                oldTab[j] = null;
                if (e.next == null)
                    newTab[e.hash & (newCap - 1)] = e;
                else if (e instanceof TreeNode)
                    ((TreeNode<K,V>)e).split(this, newTab, j, oldCap);
                else { 
                    Node<K,V> loHead = null, loTail = null;
                    Node<K,V> hiHead = null, hiTail = null;
                    Node<K,V> next;
                    do {
                        next = e.next;
                        // 原索引
                        if ((e.hash & oldCap) == 0) {
                            if (loTail == null)
                                loHead = e;
                            else
                                loTail.next = e;
                            loTail = e;
                        }
                        // 原索引+oldCap
                        else {
                            if (hiTail == null)
                                hiHead = e;
                            else
                                hiTail.next = e;
                            hiTail = e;
                        }
                    } while ((e = next) != null);
                    // 原索引放到bucket里
                    if (loTail != null) {
                        loTail.next = null;
                        newTab[j] = loHead;
                    }
                    // 原索引+oldCap放到bucket里
                    if (hiTail != null) {
                        hiTail.next = null;
                        newTab[j + oldCap] = hiHead;
                    }
                }
            }
        }
    }
    return newTab;
}
```

扩容

- 使用无参的构造方法创建HashMap对象
  - 第一次创建HashMap对象的时候，不进行扩容。在第一次put元素开始之前，调用`resize()`进行扩容。首次扩容涉及到默认的初始容量以及加载因子。第一次扩容容量`newCap`为16，存放元素个数上限`threshold`为12。

  - 之后put元素之后判断是否需要再次扩容`if (++size > threshold)`，如果需要，容量为原来的2倍`newCap = oldCap << 1`。`threshold`更新为容量的负载因子的倍数`(int)float ft = (float)newCap * loadFactor`;

- 指定初始容量参数的构造方法创建HashMap对象
  - 初始化时指定初始容量参数，`tableSizeFor(initialCapacity)`确定了`threshold`的值为大于initialCapacity参数的最小的2的n次幂,对于的数组容量为0。

  - 第一次put元素开始之前进行扩容，容量扩充为原先threshold的值`newCap = oldThr;`，`threshold`更新为容量的负载因子的倍数`(int)float ft = (float)newCap * loadFactor`;

  - 之后put元素之后判断是否需要再次扩容`if (++size > threshold)`，如果需要，容量为原来的2倍`newCap = oldCap << 1`，而`threshold`更新为容量的负载因子的倍数`(int)float ft = (float)newCap * loadFactor`;

5、rehash重新hash分配

数组扩容之后，需要重新进行hash分配

- 挨个遍历数组，将当前数组中的元素赋值给e，e节点表示了当前hash的单链表。

- 如果e.next为null,即表示e没有下一个节点，计算当前节点(以及对应的链表)对新数组的下标，将该节点移动到新数组对应的下标中。当前节点同时代表了该hash值对应的单链表。
```java
if (e.next == null)
	newTab[e.hash & (newCap - 1)] = e;
```

- 循环当前链表的元素
    - 如果`(e.hash & oldCap) == 0`表示当前元素e在新旧数组中的位置不变。使用`Node<K,V> loHead = null, loTail = null;` 表示。第一个节点为` loHead`，最后一个节点使用 `loTail` 表示。
        - 第一个节点`loHead`同时代表了整个单向链表
    - 不等于0则表示当前元素e在新旧数组中的位置已改变。`Node<K,V> hiHead = null, hiTail = null;` 表示，第一个节点为 `hiHead` ，最后一个节点使用 `hiTail` 表示。
        - 第一个节点`hiHead`同时代表了整个单向链表

`(e.hash & oldCap) == 0`表示当前元素e在新旧数组中的位置不变。原因如下：

>`oldCap`与`newCap`关系：如果`oldCap>0`则`newCap = oldCap << 1`

> 假设原先数组容量为`n`(`n`为2的倍数)。元素在旧数组的位置 `hash & (n-1)`，元素在新数组中的位置  ` hash & (2n-1)`。如果新数组与旧数组的位置相等`hash & (n-1)  == hash & (2n-1)`，则要求 `hash & n == 0`


```java
do {
		next = e.next;
		if ((e.hash & oldCap) == 0) {  //新旧数组位置不变，第一个元素为loHead，后面的node使用loTail表示
			if (loTail == null)
				loHead = e;
			else
				loTail.next = e;
			loTail = e;
		}
		else {
			if (hiTail == null)       //新旧数组位置改变，第一个元素为hiHead，后面的node链表使用hiTail表示
				hiHead = e;
			else
				hiTail.next = e;
			hiTail = e;
		}
	} while ((e = next) != null);
```


- 将当前链表的头节点添加到新数组中。如果节点在新旧位置不变则添加原先下标值的新数组中`newTab[j] = loHead`。如果节点新旧位置改变则添加到下标`j + oldCap`的新数组中。

```java
if (loTail != null) {
    loTail.next = null;
    newTab[j] = loHead;
}
if (hiTail != null) {
    hiTail.next = null;
    newTab[j + oldCap] = hiHead;  //数组扩充为原先的2倍。
}
```

##### 5. HashMap常用方法测试

```java
package map;

import java.util.Collection;
import java.util.HashMap;
import java.util.Set;

public class HashMapDemo {

    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<String, String>();
        // 键不能重复，值可以重复
        map.put("san", "张三");
        map.put("si", "李四");
        map.put("wu", "王五");
        map.put("wang", "老王");
        map.put("wang", "老王2");// 老王被覆盖
        map.put("lao", "老王");
        System.out.println("-------直接输出hashmap:-------");
        System.out.println(map);
        /**
         * 遍历HashMap
         */
        // 1.获取Map中的所有键
        System.out.println("-------foreach获取Map中所有的键:------");
        Set<String> keys = map.keySet();
        for (String key : keys) {
            System.out.print(key+"  ");
        }
        System.out.println();//换行
        // 2.获取Map中所有值
        System.out.println("-------foreach获取Map中所有的值:------");
        Collection<String> values = map.values();
        for (String value : values) {
            System.out.print(value+"  ");
        }
        System.out.println();//换行
        // 3.得到key的值的同时得到key所对应的值
        System.out.println("-------得到key的值的同时得到key所对应的值:-------");
        Set<String> keys2 = map.keySet();
        for (String key : keys2) {
            System.out.print(key + "：" + map.get(key)+"   ");

        }
        /**
         * 如果既要遍历key又要value，那么建议这种方式，因为如果先获取keySet然后再执行map.get(key)，map内部会执行两次遍历。
         * 一次是在获取keySet的时候，一次是在遍历所有key的时候。
         */
        // 当我调用put(key,value)方法的时候，首先会把key和value封装到
        // Entry这个静态内部类对象中，把Entry对象再添加到数组中，所以我们想获取
        // map中的所有键值对，我们只要获取数组中的所有Entry对象，接下来
        // 调用Entry对象中的getKey()和getValue()方法就能获取键值对了
        Set<java.util.Map.Entry<String, String>> entrys = map.entrySet();
        for (java.util.Map.Entry<String, String> entry : entrys) {
            System.out.println(entry.getKey() + "--" + entry.getValue());
        }
        
        /**
         * HashMap其他常用方法
         */
        System.out.println("after map.size()："+map.size());
        System.out.println("after map.isEmpty()："+map.isEmpty());
        System.out.println(map.remove("san"));
        System.out.println("after map.remove()："+map);
        System.out.println("after map.get(si)："+map.get("si"));
        System.out.println("after map.containsKey(si)："+map.containsKey("si"));
        System.out.println("after containsValue(李四)："+map.containsValue("李四"));
        System.out.println(map.replace("si", "李四2"));
        System.out.println("after map.replace(si, 李四2):"+map);
    }

}
```

#### 4.3. HashMap相关操作

##### 1. 多线程操作导致死循环问题

主要原因在于并发下的 Rehash 会造成元素之间会形成一个循环链表。不过，<u>jdk 1.8 后解决了这个问题</u>，但是还是不建议在多线程下使用 HashMap,因为多线程下使用 HashMap 还是会存在其他问题比如数据丢失。并发环境下推荐使用 ConcurrentHashMap 。

详情请查看：<https://coolshell.cn/articles/9606.html>

1、背景

在淘宝内网里看到同事发了贴说了一个CPU被100%的线上故障，并且这个事发生了很多次，原因是在Java语言在并发情况下使用`HashMap`造成`Race Condition`，从而导致死循环。这个事情我4、5年前也经历过，本来觉得没什么好写的，因为Java的HashMap是非线程安全的，所以在并发下必然出现问题。但是，我发现近几年，很多人都经历过这个事（在网上查“`HashMap Infinite Loop`”可以看到很多人都在说这个事）所以，觉得这个是个普遍问题，需要写篇疫苗文章说一下这个事，并且给大家看看一个完美的`“Race Condition”`是怎么形成的。

2、问题的症状

从前我们的Java代码因为一些原因使用了`HashMap`这个东西，但是当时的程序是单线程的，一切都没有问题。后来，我们的程序性能有问题，所以需要变成多线程的，于是，变成多线程后到了线上，发现程序经常占了100%的CPU，查看堆栈，你会发现程序都Hang在了`HashMap.get()`这个方法上了，重启程序后问题消失。但是过段时间又会来。而且，这个问题在测试环境里可能很难重现。


我们简单的看一下我们自己的代码，我们就知道`HashMap`被多个线程操作。而Java的文档说HashMap是非线程安全的，应该用`ConcurrentHashMap`。

但是在这里我们可以来研究一下原因

3、Hash表数据结构

我需要简单地说一下HashMap这个经典的数据结构。

`HashMap`通常会用一个指针数组（假设为`table[]`）来做分散所有的key，当一个`key`被加入时，会通过Hash算法通过`key`算出这个数组的下标`i`，然后就把这个`<key, value>`插到`table[i]`中，如果有两个不同的`key`被算在了同一个`i`，那么就叫冲突，又叫碰撞，这样会在`table[i]`上形成一个链表。


我们知道，如果`table[]`的尺寸很小，比如只有2个，如果要放进10个keys的话，那么碰撞非常频繁，于是一个`O(1)`的查找算法，就变成了链表遍历，性能变成了`O(n)`，这是Hash表的缺陷


所以，Hash表的尺寸和容量非常的重要。一般来说，Hash表这个容器当有数据要插入时，都会检查容量有没有超过设定的`thredhold`，如果超过，需要增大Hash表的尺寸，但是这样一来，整个Hash表里的无素都需要被重算一遍。这叫`rehash`，这个成本相当的大。

4、HashMap的rehash源代码 jdk1.7


**Put一个Key,Value对到Hash表中：**

```java
public V put(K key, V value)
{
    ......
    //算Hash值
    int hash = hash(key.hashCode());
    int i = indexFor(hash, table.length);
    //如果该key已被插入，则替换掉旧的value （链接操作）
    for (Entry<K,V> e = table[i]; e != null; e = e.next) {
        Object k;
        if (e.hash == hash && ((k = e.key) == key || key.equals(k))) {
            V oldValue = e.value;
            e.value = value;
            e.recordAccess(this);
            return oldValue;
        }
    }
    modCount++;
    //该key不存在，需要增加一个结点
    addEntry(hash, key, value, i);
    return null;
}
```

**扩容：**
```java
void resize(int newCapacity)
{
    Entry[] oldTable = table;
    int oldCapacity = oldTable.length;
    ......
    //创建一个新的Hash Table
    Entry[] newTable = new Entry[newCapacity];
    //将Old Hash Table上的数据迁移到New Hash Table上
    transfer(newTable);
    table = newTable;
    threshold = (int)(newCapacity * loadFactor);
}

void transfer(Entry[] newTable)
{
    Entry[] src = table;
    int newCapacity = newTable.length;
    //下面这段代码的意思是：
    //  从OldTable里摘一个元素出来，然后放到NewTable中
    for (int j = 0; j < src.length; j++) {
        Entry<K,V> e = src[j];
        if (e != null) {
            src[j] = null;
            do {
                Entry<K,V> next = e.next;
                int i = indexFor(e.hash, newCapacity);
                e.next = newTable[i];
                newTable[i] = e;
                e = next;
            } while (e != null);
        }
    }
} 
```

5、正常的ReHash的过程


我假设了我们的hash算法就是简单的用key mod 一下表的大小（也就是数组的长度）。

>正常的ReHash过程参考 `final Node<K,V>[] resize()` 源码

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115154800020.png" alt="image-20210115154800020" style="zoom: 60%;" />

* 最上面的是old hash 表，其中的Hash表的size=2, 所以key = 3, 7, 5，在mod 2以后都冲突在table[1]这里了。

* 接下来的步骤是Hash表 resize成4，然后所有的<key,value> 重新rehash的过程

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115154836301.png" alt="image-20210115154836301" style="zoom:60%;" />

* jdk1.8的rehash的过程 : 链表的顺序不会被反转

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115154905186.png" alt="image-20210115154905186" style="zoom:60%;" />

6、并发下的Rehash

假设我们有两个线程。我用红色和浅蓝色标注了一下。

线程1挂起,线程2rehash完成
```java
do {
    Entry<K,V> next = e.next; // <--假设线程一执行到这里就被调度挂起了
    int i = indexFor(e.hash, newCapacity);
    e.next = newTable[i];
    newTable[i] = e;
    e = next;
} while (e != null);
```

线程二执行完成了。于是我们有下面的这个样子。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115155028113.png" alt="image-20210115155028113" style="zoom:50%;" />

因为Thread1的 e 指向了key(3)，而next指向了key(7)，其在线程二rehash后，指向了线程二重组后的链表。我们可以看到链表的顺序被反转


线程一被调度回来执行


* 先是执行 newTalbe[i] = e;
* 然后是e = next，导致了e指向了key(7)，
* 而下一次循环的next = e.next导致了next指向了key(3)

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115155112908.png" alt="image-20210115155112908" style="zoom:50%;" />

线程一接着工作。把key(7)摘下来，放到newTable[i]的第一个，然后把e和next往下移。
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115155132478.png" alt="image-20210115155132478" style="zoom:50%;" />


环形链接出现

e.next = newTable[i] 导致  key(3).next 指向了 key(7)

注意：此时的key(7).next 已经指向了key(3)， 环形链表就这样出现了。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115155206794.png" alt="image-20210115155206794" style="zoom:50%;" />


于是，当我们的线程一调用到，HashTable.get(11)时，悲剧就出现了——Infinite Loop。

7、jdk1.8的改良。链表的顺序不会被反转

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115155233391.png" alt="image-20210115155233391" style="zoom:50%;" />



##### 2. HashMap 常见的遍历方式

###### 2.1 常见遍历方式

[HashMap 的 7 种遍历方式与性能分析！](https://mp.weixin.qq.com/s/Zz6mofCtmYpABDL1ap04ow)

随着 JDK 1.8 Streams API 的发布，使得 HashMap 拥有了更多的遍历的方式，但应该选择那种遍历方式？反而成了一个问题。

本文先从 HashMap 的遍历方法讲起，然后再从性能、原理以及安全性等方面，来分析 HashMap 各种遍历方式的优势与不足，本文主要内容如下图所示：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115155728786.png" alt="image-20210115155728786" style="zoom:50%;" />

HashMap 遍历从大的方向来说，可分为以下 4 类：

1. 迭代器（`Iterator`）方式遍历；
2. For Each 方式遍历；
3. Lambda 表达式遍历（JDK 1.8+）;
4. Streams API 遍历（JDK 1.8+）。

但每种类型下又有不同的实现方式，因此具体的遍历方式又可以分为以下 7 种：

1. 使用迭代器（Iterator）`EntrySet` 的方式进行遍历；
2. 使用迭代器（Iterator）`KeySet` 的方式进行遍历；
3. 使用 For Each `EntrySet` 的方式进行遍历；
4. 使用 For Each `KeySet` 的方式进行遍历；
5. 使用 Lambda 表达式的方式进行遍历；
6. 使用 Streams API 单线程的方式进行遍历；
7. 使用 Streams API 多线程的方式进行遍历。

接下来我们来看每种遍历方式的具体实现代码。

1、迭代器 EntrySet

```java
public class HashMapTest {
    public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
        while (iterator.hasNext()) {
            Map.Entry<Integer, String> entry = iterator.next();
            System.out.print(entry.getKey());
            System.out.print(entry.getValue());
        }
    }
}
```

以上程序的执行结果为：1 Java 2 JDK 3 Spring Framework 4 MyBatis framework 5 Java中文社群

2、迭代器 KeySet

```java
public class HashMapTest {
    public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        Iterator<Integer> iterator = map.keySet().iterator();
        while (iterator.hasNext()) {
            Integer key = iterator.next();
            System.out.print(key);
            System.out.print(map.get(key));
        }
    }
}
```

以上程序的执行结果为： 1 Java 2 JDK 3 Spring Framework 4 MyBatis framework 5 Java中文社群

3、ForEach EntrySet

```java
public class HashMapTest {
    public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.print(entry.getKey());
            System.out.print(entry.getValue());
        }
    }
}
```

以上程序的执行结果为：1 Java 2 JDK 3 Spring Framework 4 MyBatis framework 5 Java中文社群

4、ForEach KeySet

```java
public class HashMapTest {
    public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        for (Integer key : map.keySet()) {
            System.out.print(key);
            System.out.print(map.get(key));
        }
    }
}
```

以上程序的执行结果为： 1 Java 2 JDK 3 Spring Framework 4 MyBatis framework 5 Java中文社群

5、Lambda `forEach`

```java
public class HashMapTest {
    public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        map.forEach((key, value) -> {
            System.out.print(key);
            System.out.print(value);
        });
    }
}
```

以上程序的执行结果为： 1 Java 2 JDK 3 Spring Framework 4 MyBatis framework 5 Java中文社群

6、Streams API 单线程 `forEach`

```java
public class HashMapTest {
    public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        map.entrySet().stream().forEach((entry) -> {
            System.out.print(entry.getKey());
            System.out.print(entry.getValue());
        });
    }
}
```

以上程序的执行结果为：1 Java 2 JDK 3 Spring Framework 4 MyBatis framework 5 Java中文社群

7、Streams API 多线程 `forEach`

```java
public class HashMapTest {
    public static void main(String[] args) {
        // 创建并赋值 HashMap
        Map<Integer, String> map = new HashMap();
        map.put(1, "Java");
        map.put(2, "JDK");
        map.put(3, "Spring Framework");
        map.put(4, "MyBatis framework");
        map.put(5, "Java中文社群");
        // 遍历
        map.entrySet().parallelStream().forEach((entry) -> {
            System.out.print(entry.getKey());
            System.out.print(entry.getValue());
        });
    }
}
```

以上程序的执行结果为：4 MyBatis framework 5 Java中文社群 1 Java 2 JDK 3 Spring Framework

###### 2.2. JMH性能测试

接下来我们使用性能测试工具 JMH（Java Microbenchmark Harness，JAVA 微基准测试套件）来测试一下这 7 种循环的性能


首先，我们先要引入 JMH 框架，在 pom.xml 文件中添加如下配置：
```xml
<!-- https://mvnrepository.com/artifact/org.openjdk.jmh/jmh-core -->
<dependency>
    <groupId>org.openjdk.jmh</groupId>
    <artifactId>jmh-core</artifactId>
    <version>1.23</version>
</dependency>
<!-- https://mvnrepository.com/artifact/org.openjdk.jmh/jmh-generator-annprocess -->
<dependency>
    <groupId>org.openjdk.jmh</groupId>
    <artifactId>jmh-generator-annprocess</artifactId>
    <version>1.23</version>
    <scope>provided</scope>
</dependency>
```

编写jmh测试代码，如下所示：

```java
@BenchmarkMode(Mode.Throughput) // 测试类型：吞吐量
@OutputTimeUnit(TimeUnit.MILLISECONDS)
@Warmup(iterations = 2, time = 1, timeUnit = TimeUnit.SECONDS) // 预热 2 轮，每次 1s
@Measurement(iterations = 5, time = 3, timeUnit = TimeUnit.SECONDS) // 测试 5 轮，每次 3s
@State(Scope.Thread) // 每个测试线程一个实例
@Fork(1) // fork 1 个进程
public class HashMapCycle {
    static Map<Integer, String> map;

    public static void main(String[] args) throws RunnerException {
        // 启动基准测试
        Options opt = new OptionsBuilder()
                .include(HashMapCycle.class.getSimpleName()) // 要导入的测试类
                .output("F:\\study\\java-base\\jmh-map.log") // 输出测试结果的文件
                .build();
        new Runner(opt).run(); // 执行测试
    }

    @Setup(Level.Trial)
    public void initMap(){
        map = new HashMap() {{
            // 添加数据
            for (int i = 0; i < 10; i++) {
                put(i, "val:" + i);
            }
        }};
    }

    /**
     * Iterator遍历 EntrySet
     */
    @Benchmark
    public void entrySet() {
        // 遍历
        Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
        while (iterator.hasNext()) {
            Map.Entry<Integer, String> entry = iterator.next();
            System.out.println(entry.getKey());
            System.out.println(entry.getValue());
        }
    }
    /**
     * Iterator遍历 keySet
     */
    @Benchmark
    public void keySet() {
        // 遍历
        Iterator<Integer> iterator = map.keySet().iterator();
        while (iterator.hasNext()) {
            Integer key = iterator.next();
            System.out.println(key);
            System.out.println(map.get(key));
        }
    }

    /**
     * for each 遍历 EntrySet
     */
    @Benchmark
    public void forEachEntrySet() {
        // 遍历
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry.getKey());
            System.out.println(entry.getValue());
        }
    }

    /**
     * for each 遍历 KeySet
     */
    @Benchmark
    public void forEachKeySet() {
        // 遍历
        for (Integer key : map.keySet()) {
            System.out.println(key);
            System.out.println(map.get(key));
        }
    }

    /**
     * 使用 Lambda 表达式的方式进行遍历
     */
    @Benchmark
    public void lambda() {
        // 遍历
        map.forEach((key, value) -> {
            System.out.println(key);
            System.out.println(value);
        });
    }

    /**
     * 使用 Streams API 单线程的方式进行遍历；
     */
    @Benchmark
    public void streamApi() {
        // 单线程遍历
        map.entrySet().stream().forEach((entry) -> {
            System.out.println(entry.getKey());
            System.out.println(entry.getValue());
        });
    }

    /**
     * 使用 Streams API 多线程的方式进行遍历。
     */
    @Benchmark
    public void parallelStreamApi() {
        // 多线程遍历
        map.entrySet().parallelStream().forEach((entry) -> {
            System.out.println(entry.getKey());
            System.out.println(entry.getValue());
        });
    }
}
```

执行结果：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115160057019.png" alt="image-20210115160057019" style="zoom:50%;" />

其中 Score 列表示每秒执行操作数(吞吐量)， ± 符号表示误差。从以上结果可以看出，如果加上后面的误差值的话，可以得出的结论是，上面6种遍历方法在性能方面几乎没有任何差别。

>为什么`parallelStream`并发遍历和`stream`串行遍历吞吐量差不多

>parallelStream默认使用了fork-join框架，其默认线程数是CPU核心数。修改默认的多线程数量，在运行代码之前，加入如下代码： ` System.setProperty("java.util.concurrent.ForkJoinPool.common.parallelism", "10"); ` 


###### 2.3. 性能原理分析

要理解性能测试的结果，我们需要把所有遍历代码通过 javac，编译成字节码来看具体的原因，编译之后我们使用 Idea 打开字节码信息，内容如下：


通过迭代器循环和 for 循环的遍历的 EntrySet 最终生成的代码是一样的，他们都是在循环中创建了一个遍历对象 Entry ，如下所示：

```java
public void entrySet() {
	Iterator iterator = map.entrySet().iterator();

	while(iterator.hasNext()) {
		Entry<Integer, String> entry = (Entry)iterator.next();
		System.out.println(entry.getKey());
		System.out.println((String)entry.getValue());
	}

}

public void forEachEntrySet() {
	Iterator var1 = map.entrySet().iterator();

	while(var1.hasNext()) {
		Entry<Integer, String> entry = (Entry)var1.next();
		System.out.println(entry.getKey());
		System.out.println((String)entry.getValue());
	}

}
```

通过迭代器和 for 循环遍历的 KeySet 代码也是一样的，如下所示：
```java
public void keySet() {
	Iterator iterator = map.keySet().iterator();

	while(iterator.hasNext()) {
		Integer key = (Integer)iterator.next();
		System.out.println(key);
		System.out.println((String)map.get(key));
	}

}

public void forEachKeySet() {
	Iterator var1 = map.keySet().iterator();

	while(var1.hasNext()) {
		Integer key = (Integer)var1.next();
		System.out.println(key);
		System.out.println((String)map.get(key));
	}

}
```

可以看出 KeySet 在循环中创建了一个 Integer 的局部变量，并且值是从 map 对象中直接获取的。

所以通过字节码来看，使用 EntrySet 和 KeySet 代码差别不是很大，并不像网上说的那样 KeySet 的性能远不如 EntrySet，因此从性能的角度来说 EntrySet 和 KeySet 几乎是相近的，但从代码的优雅型和可读性来说，还是推荐使用 EntrySet。

###### 2.4. 安全性测试

我们把以上遍历划分为四类进行测试：迭代器方式、For 循环方式、Lambda 方式和 Stream 方式，测试代码如下。

1、迭代器方式

```java
Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
while (iterator.hasNext()) {
    Map.Entry<Integer, String> entry = iterator.next();
    if (entry.getKey() == 1) {
        // 删除
        System.out.println("del:" + entry.getKey());
        iterator.remove();
    } else {
        System.out.println("show:" + entry.getKey());
    }
}
```

以上程序的执行结果：
```
show:0
del:1
show:2
```

测试结果：**迭代器中循环删除数据安全**

2、For 循环方式

```java
for (Map.Entry<Integer, String> entry : map.entrySet()) {
    if (entry.getKey() == 1) {
        // 删除
        System.out.println("del:" + entry.getKey());
        map.remove(entry.getKey());
    } else {
        System.out.println("show:" + entry.getKey());
    }
}
```

以上程序的执行结果：
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115160237893.png" alt="image-20210115160237893" style="zoom:40%;" />


测试结果：For 循环中删除数据非安全

3、Lambda 方式

```java
map.forEach((key, value) -> {
    if (key == 1) {
        System.out.println("del:" + key);
        map.remove(key);
    } else {
        System.out.println("show:" + key);
    }
});
```

以上程序的执行结果：
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115160312484.png" alt="image-20210115160312484" style="zoom:40%;" />


测试结果：Lambda 循环中删除数据非安全。

**Lambda 删除的正确方式：**

```java
// 根据 map 中的 key 去判断删除
map.keySet().removeIf(key -> key == 1);

map.forEach((key, value) -> {
    System.out.println("show:" + key);
});
```

以上程序的执行结果：
```
show:0
show:2
```

>从上面的代码可以看出，可以先使用 Lambda 的 removeIf 删除多余的数据，再进行循环是一种正确操作集合的方式。

4、Stream 方式

```java
map.entrySet().stream().forEach((entry) -> {
    if (entry.getKey() == 1) {
        System.out.println("del:" + entry.getKey());
        map.remove(entry.getKey());
    } else {
        System.out.println("show:" + entry.getKey());
    }
});
```

以上程序的执行结果：
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115160418600.png" alt="image-20210115160418600" style="zoom:40%;" />


测试结果：Stream 循环中删除数据非安全。

**Stream 循环的正确方式：**

```java
map.entrySet().stream().filter(m -> 1 != m.getKey()).forEach((entry) -> {
    if (entry.getKey() == 1) {
        System.out.println("del:" + entry.getKey());
    } else {
        System.out.println("show:" + entry.getKey());
    }
});
```

以上程序的执行结果：
```
show:0
show:2
```

>从上面的代码可以看出，可以使用 Stream 中的 filter 过滤掉无用的数据，再进行遍历也是一种安全的操作集合的方式。

5、小结

我们不能在遍历中使用集合 `map.remove()` 来删除数据，这是非安全的操作方式，但我们可以使用迭代器的` iterator.remove()` 的方法来删除数据，这是安全的删除集合的方式。同样的我们也可以使用 Lambda 中的 `removeIf` 来提前删除数据，或者是使用 Stream 中的` filter `过滤掉要删除的数据进行循环，这样都是安全的，当然我们也可以在 for 循环前删除数据再遍历也是线程安全的。

###### 2.5. 总结

- 
  本文我们讲了 HashMap 4 大类（迭代器、for、lambda、stream）遍历方式，以及具体的 7 种遍历方法，除了 Stream 的并行循环，其他几种遍历方法的性能差别不大，但从简洁性和优雅性上来看，**Lambda 和 Stream 无疑是最适合的遍历方式**。

- 
  从「安全性」方面测试了 4 大类遍历结果，从安全性来讲，我们应该使用迭代器提供的 iterator.remove() 方法来进行删除，这种方式是安全的在遍历中删除集合的方式，或者使用 Stream 中的 filter 过滤掉要删除的数据再进行循环，也是安全的操作方式。当然我们也可以在 for 循环前删除数据

#### 4.4. ConcurrentHashMap

##### 1. 与Hashtable

ConcurrentHashMap 和 Hashtable 的区别主要体现在实现线程安全的方式上不同。

- 底层数据结构：
  - `ConcurrentHashMap` : JDK1.7 的 ConcurrentHashMap 底层采用 **分段的数组+链表** 实现，JDK1.8 采用的数据结构跟 HashMap1.8 的结构一样，**数组+链表/红黑二叉树**。
  - `Hashtable`：Hashtable 和 JDK1.8 之前的 HashMap 的底层数据结构类似都是采用 **数组+链表** 的形式，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的；

- 
  实现线程安全的方式（重要）：
  - `ConcurrentHashMap` :  ① 在 JDK1.7 的时候，ConcurrentHashMap（分段锁） 对整个桶数组进行了分割分段(Segment)，每一把锁只锁容器其中一部分数据，多线程访问容器里不同数据段的数据，就不会存在锁竞争，提高并发访问率。 到了 JDK1.8 的时候已经摒弃了 Segment 的概念，而是直接用 Node数组+链表+红黑树 的数据结构来实现，并发控制使用 synchronized 和 CAS 来操作。（JDK1.6 以后 对 synchronized 锁做了很多优化） 整个看起来就像是优化过且线程安全的 HashMap，虽然在 JDK1.8 中还能看到 Segment 的数据结构，但是已经简化了属性，只是为了兼容旧版本；
  - `Hashtable`：Hashtable(同一把锁) ，使用 synchronized 来保证线程安全，效率非常低下。当一个线程访问同步方法时，其他线程也访问同步方法，可能会进入阻塞或轮询状态，如使用 put 添加元素，另一个线程不能使用 put 添加元素，也不能使用 get，竞争会越来越激烈效率越低。


两者的对比图：

HashTable:

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115161021180.png" alt="image-20210115161021180" style="zoom:60%;" />

JDK1.7 的 ConcurrentHashMap：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115161041543.png" alt="image-20210115161041543" style="zoom:60%;" />


JDK1.8 的 ConcurrentHashMap：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115161102761.png" alt="image-20210115161102761" style="zoom:60%;" />

JDK1.8 的 `ConcurrentHashMap` 不再是 Segment 数组 + HashEntry 数组 + 链表，而是 Node 数组 + 链表 / 红黑树。不过，Node 只能用于链表的情况，红黑树的情况需要使用 `TreeNode`。当冲突链表达到一定长度时，链表会转换成红黑树。


##### 2. 线程安全的底层实现方式

1、JDK1.7（上面有示意图）

首先将数据分为一段一段的存储，然后给每一段数据配一把锁，当一个线程占用锁访问其中一个段数据时，其他段的数据也能被其他线程访问。

ConcurrentHashMap 是由 Segment 数组结构和 HashEntry 数组结构组成。

Segment 实现了 ReentrantLock,所以 Segment 是一种可重入锁，扮演锁的角色。HashEntry 用于存储键值对数据。

```java
static class Segment<K,V> extends ReentrantLock implements Serializable {
}
```

一个 ConcurrentHashMap 里包含一个 Segment 数组。Segment 的结构和 HashMap 类似，是一种数组和链表结构，一个 Segment 包含一个 HashEntry 数组，每个 HashEntry 是一个链表结构的元素，每个 Segment 守护着一个 HashEntry 数组里的元素，当对 HashEntry 数组的数据进行修改时，必须首先获得对应的 Segment 的锁。

2、JDK1.8 （上面有示意图）

ConcurrentHashMap 取消了 Segment 分段锁，采用 CAS 和 synchronized 来保证并发安全。数据结构跟 HashMap1.8 的结构类似，数组+链表/红黑二叉树。Java 8 在链表长度超过一定阈值（8）时将链表（寻址时间复杂度为 O(N)）转换为红黑树（寻址时间复杂度为 O(log(N))）

>synchronized 只锁定当前链表或红黑二叉树的首节点，这样只要 hash 不冲突，就不会产生并发，效率又提升 N 倍。

##### 3. 源码分析

###### 3.1. 1.7源码

1、存储结构

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115161316787.png" alt="image-20210115161316787" style="zoom:60%;" />

Java 7 中 ConcurrentHashMap 的存储结构如上图，ConcurrnetHashMap 由很多个 Segment  组合，而每一个 Segment 是一个类似于 HashMap 的结构，所以每一个 HashMap 的内部可以进行扩容。但是 Segment 的个数一旦初始化就不能改变，默认 Segment 的个数是 16 个，你也可以认为 ConcurrentHashMap 默认支持最多 16 个线程并发。

2、初始化

通过 ConcurrentHashMap 的无参构造探寻 ConcurrentHashMap 的初始化流程。

```java
    /**
     * Creates a new, empty map with a default initial capacity (16),
     * load factor (0.75) and concurrencyLevel (16).
     */
    public ConcurrentHashMap() {
        this(DEFAULT_INITIAL_CAPACITY, DEFAULT_LOAD_FACTOR, DEFAULT_CONCURRENCY_LEVEL);
    }
```

无参构造中调用了有参构造，传入了三个参数的默认值，他们的值是。

```java
    /**
     * 默认初始化容量
     */
    static final int DEFAULT_INITIAL_CAPACITY = 16;

    /**
     * 默认负载因子
     */
    static final float DEFAULT_LOAD_FACTOR = 0.75f;

    /**
     * 默认并发级别
     */
    static final int DEFAULT_CONCURRENCY_LEVEL = 16;
    
    /**
     * segment最小容量
     */
    static final int MIN_SEGMENT_TABLE_CAPACITY = 2;

```

接着看下这个有参构造函数的内部实现逻辑。

```java
@SuppressWarnings("unchecked")
public ConcurrentHashMap(int initialCapacity,float loadFactor, int concurrencyLevel) {
    // 参数校验
    if (!(loadFactor > 0) || initialCapacity < 0 || concurrencyLevel <= 0)
        throw new IllegalArgumentException();
    // 校验并发级别大小，大于 1<<16，重置为 65536
    if (concurrencyLevel > MAX_SEGMENTS)
        concurrencyLevel = MAX_SEGMENTS;
    // Find power-of-two sizes best matching arguments
    // 2的多少次方
    int sshift = 0;
    int ssize = 1;
    // 这个循环可以找到 concurrencyLevel 之上最近的 2的次方值
    while (ssize < concurrencyLevel) {
        ++sshift;
        ssize <<= 1;
    }
    // 记录段偏移量
    this.segmentShift = 32 - sshift;
    // 记录段掩码
    this.segmentMask = ssize - 1;
    // 设置容量
    if (initialCapacity > MAXIMUM_CAPACITY)
        initialCapacity = MAXIMUM_CAPACITY;
    // c = 容量 / ssize ，默认 16 / 16 = 1，这里是计算每个 Segment 中的类似于 HashMap 的容量
    int c = initialCapacity / ssize;
    if (c * ssize < initialCapacity)
        ++c;
    int cap = MIN_SEGMENT_TABLE_CAPACITY;
    //Segment 中的类似于 HashMap 的容量至少是2或者2的倍数
    while (cap < c)
        cap <<= 1;
    // create segments and segments[0]
    // 创建 Segment 数组，设置 segments[0]
    Segment<K,V> s0 = new Segment<K,V>(loadFactor, (int)(cap * loadFactor),
                         (HashEntry<K,V>[])new HashEntry[cap]);
    Segment<K,V>[] ss = (Segment<K,V>[])new Segment[ssize];
    UNSAFE.putOrderedObject(ss, SBASE, s0); // ordered write of segments[0]
    this.segments = ss;
}
```

总结一下在 Java 7 中 ConcurrnetHashMap 的初始化逻辑。

1. 必要参数校验。
2. 校验并发级别 concurrencyLevel 大小，如果大于最大值，重置为最大值。无参构造并发级别 默认值是 16.

```java
// 校验并发级别大小，大于 1<<16，重置为 65536
if (concurrencyLevel > MAX_SEGMENTS)
    concurrencyLevel = MAX_SEGMENTS;
```

3. 寻找并发级别 concurrencyLevel 之上最近的 2 的幂次方值，作为segment个数大小`ssize`，默认是 16个segment。

```java
// 2的多少次方
int sshift = 0;
int ssize = 1;
// 这个循环可以找到 concurrencyLevel 之上最近的 2的次方值
while (ssize < concurrencyLevel) {
    ++sshift;
    ssize <<= 1;
}
```

4. 记录 `segmentShift` 偏移量，这个值为【容量 =  2 的N次方】中的 N，在后面 Put 时计算位置时会用到。默认是 32 - sshift = 28 sshift为4
```java
// 2的多少次方
int sshift = 0;
int ssize = 1;
// 这个循环可以找到 concurrencyLevel 之上最近的 2的次方值
while (ssize < concurrencyLevel) {
    ++sshift;
    ssize <<= 1;
}
// 记录段偏移量
this.segmentShift = 32 - sshift;
```


5. 记录 `segmentMask`，默认是` ssize - 1` = 16 -1 = 15.
```java
// 记录段掩码
this.segmentMask = ssize - 1;
```

6. 计算每个 Segment 中的类似于 HashMap 的容量。初始容量`initialCapacity`除以segment个数`ssize`得到结果`c`，如果有余数则`++c`。如果最小容量小于计算的容量`c`则将最小容量进行右移扩容，扩容之后作为segment的容量。


默认` ssize` ：16  `initialCapacity`  ：16   默认的segment容量为`MIN_SEGMENT_TABLE_CAPACITY` ： 2

```java
int c = initialCapacity / ssize;
if (c * ssize < initialCapacity)
    ++c;
int cap = MIN_SEGMENT_TABLE_CAPACITY;
//Segment 中的类似于 HashMap 的容量至少是2或者2的倍数
while (cap < c)
    cap <<= 1;
```

7. 初始化 segments[0]，默认大小为 2，负载因子 0.75，扩容阀值是 2*0.75=1.5，插入第二个值时才会进行扩容。

```java
  // 创建 Segment 数组，设置 segments[0]
    Segment<K,V> s0 = new Segment<K,V>(loadFactor, (int)(cap * loadFactor),
                         (HashEntry<K,V>[])new HashEntry[cap]);
    Segment<K,V>[] ss = (Segment<K,V>[])new Segment[ssize];
    UNSAFE.putOrderedObject(ss, SBASE, s0); // ordered write of segments[0]
    this.segments = ss;
```

3、put

接着上面的初始化参数继续查看 put 方法源码。

```java
/**
 * Maps the specified key to the specified value in this table.
 * Neither the key nor the value can be null.
 *
 * <p> The value can be retrieved by calling the <tt>get</tt> method
 * with a key that is equal to the original key.
 *
 * @param key key with which the specified value is to be associated
 * @param value value to be associated with the specified key
 * @return the previous value associated with <tt>key</tt>, or
 *         <tt>null</tt> if there was no mapping for <tt>key</tt>
 * @throws NullPointerException if the specified key or value is null
 */
public V put(K key, V value) {
    Segment<K,V> s;
    if (value == null)
        throw new NullPointerException();
    int hash = hash(key);
    // hash 值无符号右移 28位（初始化时获得），然后与 segmentMask=15 做与运算
    // 其实也就是把高4位与segmentMask（1111）做与运算
    int j = (hash >>> segmentShift) & segmentMask;
    if ((s = (Segment<K,V>)UNSAFE.getObject          // nonvolatile; recheck
         (segments, (j << SSHIFT) + SBASE)) == null) //  in ensureSegment
        // 如果查找到的 Segment 为空，初始化
        s = ensureSegment(j);
    return s.put(key, hash, value, false);
}

/**
 * Returns the segment for the given index, creating it and
 * recording in segment table (via CAS) if not already present.
 *
 * @param k the index
 * @return the segment
 */
@SuppressWarnings("unchecked")
private Segment<K,V> ensureSegment(int k) {
    final Segment<K,V>[] ss = this.segments;
    long u = (k << SSHIFT) + SBASE; // raw offset
    Segment<K,V> seg;
    // 判断 u 位置的 Segment 是否为null
    if ((seg = (Segment<K,V>)UNSAFE.getObjectVolatile(ss, u)) == null) {
        Segment<K,V> proto = ss[0]; // use segment 0 as prototype
        // 获取0号 segment 里的 HashEntry<K,V> 初始化长度
        int cap = proto.table.length;
        // 获取0号 segment 里的 hash 表里的扩容负载因子，所有的 segment 的 loadFactor 是相同的
        float lf = proto.loadFactor;
        // 计算扩容阀值
        int threshold = (int)(cap * lf);
        // 创建一个 cap 容量的 HashEntry 数组
        HashEntry<K,V>[] tab = (HashEntry<K,V>[])new HashEntry[cap];
        if ((seg = (Segment<K,V>)UNSAFE.getObjectVolatile(ss, u)) == null) { // recheck
            // 再次检查 u 位置的 Segment 是否为null，因为这时可能有其他线程进行了操作
            Segment<K,V> s = new Segment<K,V>(lf, threshold, tab);
            // 自旋检查 u 位置的 Segment 是否为null
            while ((seg = (Segment<K,V>)UNSAFE.getObjectVolatile(ss, u))
                   == null) {
                // 使用CAS 赋值，只会成功一次
                if (UNSAFE.compareAndSwapObject(ss, u, null, seg = s))
                    break;
            }
        }
    }
    return seg;
}
```

上面的源码分析了 ConcurrentHashMap 在 put 一个数据时的处理流程，下面梳理下具体流程。

1. 计算要 put 的 key 的位置，获取指定位置的 Segment。

2. 如果指定位置的 Segment 为空，则初始化这个 Segment.

   初始化 Segment 流程：

   1. 检查计算得到的位置的 Segment 是否为null.
   2. 为 null 继续初始化，使用 Segment[0] 的容量和负载因子创建一个 HashEntry 数组。
   3. 再次检查计算得到的指定位置的 Segment 是否为null.
   4. 使用创建的 HashEntry 数组初始化这个 Segment.
   5. 自旋判断计算得到的指定位置的 Segment 是否为null，使用 CAS 在这个位置赋值为 Segment.

3. Segment.put 插入 key,value 值。

上面探究了获取 Segment 段和初始化 Segment 段的操作。最后一行的 Segment 的 put 方法还没有查看，继续分析。

```java
final V put(K key, int hash, V value, boolean onlyIfAbsent) {
    // 获取 ReentrantLock 独占锁，获取不到，scanAndLockForPut 获取。
    HashEntry<K,V> node = tryLock() ? null : scanAndLockForPut(key, hash, value);
    V oldValue;
    try {
        HashEntry<K,V>[] tab = table;
        // 计算要put的数据位置
        int index = (tab.length - 1) & hash;
        // CAS 获取 index 坐标的值
        HashEntry<K,V> first = entryAt(tab, index);
        for (HashEntry<K,V> e = first;;) {
            if (e != null) {
                // 检查是否 key 已经存在，如果存在，则遍历链表寻找位置，找到后替换 value
                K k;
                if ((k = e.key) == key ||
                    (e.hash == hash && key.equals(k))) {
                    oldValue = e.value;
                    if (!onlyIfAbsent) {
                        e.value = value;
                        ++modCount;
                    }
                    break;
                }
                e = e.next;
            }
            else {
                // first 有值没说明 index 位置已经有值了，有冲突，链表头插法。
                if (node != null)
                    node.setNext(first);
                else
                    node = new HashEntry<K,V>(hash, key, value, first);
                int c = count + 1;
                // 容量大于扩容阀值，小于最大容量，进行扩容
                if (c > threshold && tab.length < MAXIMUM_CAPACITY)
                    rehash(node);
                else
                    // index 位置赋值 node，node 可能是一个元素，也可能是一个链表的表头
                    setEntryAt(tab, index, node);
                ++modCount;
                count = c;
                oldValue = null;
                break;
            }
        }
    } finally {
        unlock();
    }
    return oldValue;
}
```

由于 Segment 继承了 ReentrantLock，所以 Segment 内部可以很方便的获取锁，put 流程就用到了这个功能。

1. tryLock() 获取锁，获取不到使用  `scanAndLockForPut` 方法继续获取。

2. 计算 put 的数据要放入的 index 位置，然后获取这个位置上的 HashEntry 。

3. 遍历 put 新元素，为什么要遍历？因为这里获取的 HashEntry 可能是一个空元素，也可能是链表已存在，所以要区别对待。

   如果这个位置上的 HashEntry 不存在：

   1. 如果当前容量大于扩容阀值，小于最大容量，进行扩容。
   2. 直接头插法插入。

   如果这个位置上的 HashEntry 存在：

   1. 判断链表当前元素 Key 和 hash 值是否和要 put 的 key 和 hash 值一致。一致则替换值
   2. 不一致，获取链表下一个节点，直到发现相同进行值替换，或者链表表里完毕没有相同的。
      1. 如果当前容量大于扩容阀值，小于最大容量，进行扩容。
      2. 直接链表头插法插入。

4. 如果要插入的位置之前已经存在，替换后返回旧值，否则返回 null.

这里面的第一步中的 scanAndLockForPut 操作这里没有介绍，这个方法做的操作就是不断的自旋 `tryLock()` 获取锁。当自旋次数大于指定次数时，使用 `lock()` 阻塞获取锁。在自旋时顺表获取下 hash 位置的 HashEntry。

```java
private HashEntry<K,V> scanAndLockForPut(K key, int hash, V value) {
    HashEntry<K,V> first = entryForHash(this, hash);
    HashEntry<K,V> e = first;
    HashEntry<K,V> node = null;
    int retries = -1; // negative while locating node
    // 自旋获取锁
    while (!tryLock()) {
        HashEntry<K,V> f; // to recheck first below
        if (retries < 0) {
            if (e == null) {
                if (node == null) // speculatively create node
                    node = new HashEntry<K,V>(hash, key, value, null);
                retries = 0;
            }
            else if (key.equals(e.key))
                retries = 0;
            else
                e = e.next;
        }
        else if (++retries > MAX_SCAN_RETRIES) {
            // 自旋达到指定次数后，阻塞等到只到获取到锁
            lock();
            break;
        }
        else if ((retries & 1) == 0 &&
                 (f = entryForHash(this, hash)) != first) {
            e = first = f; // re-traverse if entry changed
            retries = -1;
        }
    }
    return node;
}

```

4、扩容 rehash

ConcurrentHashMap 的扩容只会扩容到原来的两倍。老数组里的数据移动到新的数组时，位置要么不变，要么变为 index+ oldSize，参数里的 node 会在扩容之后使用链表**头插法**插入到指定位置。

```java
private void rehash(HashEntry<K,V> node) {
    HashEntry<K,V>[] oldTable = table;
    // 老容量
    int oldCapacity = oldTable.length;
    // 新容量，扩大两倍
    int newCapacity = oldCapacity << 1;
    // 新的扩容阀值 
    threshold = (int)(newCapacity * loadFactor);
    // 创建新的数组
    HashEntry<K,V>[] newTable = (HashEntry<K,V>[]) new HashEntry[newCapacity];
    // 新的掩码，默认2扩容后是4，-1是3，二进制就是11。
    int sizeMask = newCapacity - 1;
    for (int i = 0; i < oldCapacity ; i++) {
        // 遍历老数组
        HashEntry<K,V> e = oldTable[i];
        if (e != null) {
            HashEntry<K,V> next = e.next;
            // 计算新的位置，新的位置只可能是不便或者是老的位置+老的容量。
            int idx = e.hash & sizeMask;
            if (next == null)   //  Single node on list
                // 如果当前位置还不是链表，只是一个元素，直接赋值
                newTable[idx] = e;
            else { // Reuse consecutive sequence at same slot
                // 如果是链表了
                HashEntry<K,V> lastRun = e;
                int lastIdx = idx;
                // 新的位置只可能是不便或者是老的位置+老的容量。
                // 遍历结束后，lastRun 后面的元素位置都是相同的
                for (HashEntry<K,V> last = next; last != null; last = last.next) {
                    int k = last.hash & sizeMask;
                    if (k != lastIdx) {
                        lastIdx = k;
                        lastRun = last;
                    }
                }
                // ，lastRun 后面的元素位置都是相同的，直接作为链表赋值到新位置。
                newTable[lastIdx] = lastRun;
                // Clone remaining nodes
                for (HashEntry<K,V> p = e; p != lastRun; p = p.next) {
                    // 遍历剩余元素，头插法到指定 k 位置。
                    V v = p.value;
                    int h = p.hash;
                    int k = h & sizeMask;
                    HashEntry<K,V> n = newTable[k];
                    newTable[k] = new HashEntry<K,V>(h, p.key, v, n);
                }
            }
        }
    }
    // 头插法插入新的节点
    int nodeIndex = node.hash & sizeMask; // add the new node
    node.setNext(newTable[nodeIndex]);
    newTable[nodeIndex] = node;
    table = newTable;
}
```

有些同学可能会对最后的两个 for 循环有疑惑，这里第一个 for 是为了寻找这样一个节点，这个节点后面的所有 next 节点的新位置都是相同的。然后把这个作为一个链表赋值到新位置。第二个 for 循环是为了把剩余的元素通过头插法插入到指定位置链表。这样实现的原因可能是基于概率统计，有深入研究的同学可以发表下意见。

5、get

到这里就很简单了，get 方法只需要两步即可。

1. 计算得到 key 的存放位置。
2. 遍历指定位置查找相同 key 的 value 值。

```java
public V get(Object key) {
    Segment<K,V> s; // manually integrate access methods to reduce overhead
    HashEntry<K,V>[] tab;
    int h = hash(key);
    long u = (((h >>> segmentShift) & segmentMask) << SSHIFT) + SBASE;
    // 计算得到 key 的存放位置
    if ((s = (Segment<K,V>)UNSAFE.getObjectVolatile(segments, u)) != null &&
        (tab = s.table) != null) {
        for (HashEntry<K,V> e = (HashEntry<K,V>) UNSAFE.getObjectVolatile
                 (tab, ((long)(((tab.length - 1) & h)) << TSHIFT) + TBASE);
             e != null; e = e.next) {
            // 如果是链表，遍历查找到相同 key 的 value。
            K k;
            if ((k = e.key) == key || (e.hash == h && key.equals(k)))
                return e.value;
        }
    }
    return null;
}
```

###### 3.2. 1.8源码

1、存储结构

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115161617176.png" alt="image-20210115161617176" style="zoom:60%;" />


可以发现 Java8 的 ConcurrentHashMap  相对于 Java7 来说变化比较大，不再是之前的 Segment 数组 + HashEntry 数组 + 链表，而是 Node 数组 + 链表 / 红黑树。当冲突链表达到一定长度时，链表会转换成红黑树。

2、初始化 initTable

```java
/**
 * Initializes table, using the size recorded in sizeCtl.
 */
private final Node<K,V>[] initTable() {
    Node<K,V>[] tab; int sc;
    while ((tab = table) == null || tab.length == 0) {
        ／／　如果 sizeCtl < 0 ,说明另外的线程执行CAS 成功，正在进行初始化。
        if ((sc = sizeCtl) < 0)
            // 让出 CPU 使用权
            Thread.yield(); // lost initialization race; just spin
        else if (U.compareAndSwapInt(this, SIZECTL, sc, -1)) {
            try {
                if ((tab = table) == null || tab.length == 0) {
                    int n = (sc > 0) ? sc : DEFAULT_CAPACITY;
                    @SuppressWarnings("unchecked")
                    Node<K,V>[] nt = (Node<K,V>[])new Node<?,?>[n];
                    table = tab = nt;
                    sc = n - (n >>> 2);
                }
            } finally {
                sizeCtl = sc;
            }
            break;
        }
    }
    return tab;
}
```

从源码中可以发现 ConcurrentHashMap 的初始化是通过**自旋和 CAS** 操作完成的。里面需要注意的是变量 `sizeCtl` ，它的值决定着当前的初始化状态。

1. -1  说明正在初始化
2. -N 说明有N-1个线程正在进行扩容
3. 表示 table 初始化大小，如果 table 没有初始化
4. 表示 table 容量，如果 table　已经初始化。

3、put

直接过一遍 put 源码。

```java
public V put(K key, V value) {
    return putVal(key, value, false);
}

/** Implementation for put and putIfAbsent */
final V putVal(K key, V value, boolean onlyIfAbsent) {
    // key 和 value 不能为空
    if (key == null || value == null) throw new NullPointerException();
    int hash = spread(key.hashCode());
    int binCount = 0;
    for (Node<K,V>[] tab = table;;) {
        // f = 目标位置元素
        Node<K,V> f; int n, i, fh;// fh 后面存放目标位置的元素 hash 值
        if (tab == null || (n = tab.length) == 0)
            // 数组桶为空，初始化数组桶（自旋+CAS)
            tab = initTable();
        else if ((f = tabAt(tab, i = (n - 1) & hash)) == null) {
            // 桶内为空，CAS 放入，不加锁，成功了就直接 break 跳出
            if (casTabAt(tab, i, null,new Node<K,V>(hash, key, value, null)))
                break;  // no lock when adding to empty bin
        }
        else if ((fh = f.hash) == MOVED)
            tab = helpTransfer(tab, f);
        else {
            V oldVal = null;
            // 使用 synchronized 加锁加入节点
            synchronized (f) {
                if (tabAt(tab, i) == f) {
                    // 说明是链表
                    if (fh >= 0) {
                        binCount = 1;
                        // 循环加入新的或者覆盖节点
                        for (Node<K,V> e = f;; ++binCount) {
                            K ek;
                            if (e.hash == hash &&
                                ((ek = e.key) == key ||
                                 (ek != null && key.equals(ek)))) {
                                oldVal = e.val;
                                if (!onlyIfAbsent)
                                    e.val = value;
                                break;
                            }
                            Node<K,V> pred = e;
                            if ((e = e.next) == null) {
                                pred.next = new Node<K,V>(hash, key,
                                                          value, null);
                                break;
                            }
                        }
                    }
                    else if (f instanceof TreeBin) {
                        // 红黑树
                        Node<K,V> p;
                        binCount = 2;
                        if ((p = ((TreeBin<K,V>)f).putTreeVal(hash, key,
                                                       value)) != null) {
                            oldVal = p.val;
                            if (!onlyIfAbsent)
                                p.val = value;
                        }
                    }
                }
            }
            if (binCount != 0) {
                if (binCount >= TREEIFY_THRESHOLD)
                    treeifyBin(tab, i);
                if (oldVal != null)
                    return oldVal;
                break;
            }
        }
    }
    addCount(1L, binCount);
    return null;
}
```

1. 根据 key 计算出 hashcode 。

2. 判断是否需要进行初始化。

3. 即为当前 key 定位出的 Node，如果为空表示当前位置可以写入数据，利用 CAS 尝试写入，失败则自旋保证成功。

4. 如果当前位置的 `hashcode == MOVED == -1`,则需要进行扩容。

5. 如果都不满足，则利用 synchronized 锁写入数据。

6. 如果数量大于 `TREEIFY_THRESHOLD` 则要转换为红黑树。

4、get

get 流程比较简单，直接过一遍源码。

```java
public V get(Object key) {
    Node<K,V>[] tab; Node<K,V> e, p; int n, eh; K ek;
    // key 所在的 hash 位置
    int h = spread(key.hashCode());
    if ((tab = table) != null && (n = tab.length) > 0 &&
        (e = tabAt(tab, (n - 1) & h)) != null) {
        // 如果指定位置元素存在，头结点hash值相同
        if ((eh = e.hash) == h) {
            if ((ek = e.key) == key || (ek != null && key.equals(ek)))
                // key hash 值相等，key值相同，直接返回元素 value
                return e.val;
        }
        else if (eh < 0)
            // 头结点hash值小于0，说明正在扩容或者是红黑树，find查找
            return (p = e.find(h, key)) != null ? p.val : null;
        while ((e = e.next) != null) {
            // 是链表，遍历查找
            if (e.hash == h &&
                ((ek = e.key) == key || (ek != null && key.equals(ek))))
                return e.val;
        }
    }
    return null;
}
```

总结一下 get 过程：

1. 根据 hash 值计算位置。
2. 查找到指定位置，如果头节点就是要找的，直接返回它的 value.
3. 如果头节点 hash 值小于 0 ，说明正在扩容或者是红黑树，查找之。
4. 如果是链表，遍历查找之。

总结：

总的来说 ConcruuentHashMap 在 Java8 中相对于 Java7 来说变化还是挺大的，

###### 3.3.  总结

Java7 中 ConcruuentHashMap 使用的分段锁，也就是每一个 Segment 上同时只有一个线程可以操作，每一个 Segment 都是一个类似 HashMap 数组的结构，它可以扩容，它的冲突会转化为链表。但是 Segment 的个数一但初始化就不能改变。

Java8 中的 ConcruuentHashMap  使用的 Synchronized 锁加 CAS 的机制。结构也由 Java7 中的 Segment 数组 + HashEntry 数组 + 链表 进化成了  Node 数组 + 链表 / 红黑树，Node 是类似于一个 HashEntry 的结构。它的冲突再达到一定大小时会转化成红黑树，在冲突小于一定数量时又退回链表。

有些同学可能对 Synchronized 的性能存在疑问，其实 Synchronized 锁自从引入锁升级策略后，性能不再是问题，有兴趣的同学可以自己了解下 Synchronized 的锁升级。ConcurrentHashMap源码分析

### 5. Collections工具类

Collections 工具类常用方法:

1. 排序
2. 查找,替换操作
3. 同步控制(不推荐，需要线程安全的集合类型时请考虑使用 JUC 包下的并发集合)

#### 5.1. 排序操作

```java
void reverse(List list)//反转
void shuffle(List list)//随机排序
void sort(List list)//按自然排序的升序排序
void sort(List list, Comparator c)//定制排序，由Comparator控制排序逻辑
void swap(List list, int i , int j)//交换两个索引位置的元素
void rotate(List list, int distance)//旋转。当distance为正数时，将list后distance个元素整体移到前面。当distance为负数时，将 list的前distance个元素整体移到后面
```

#### 5.2. 查找,替换操作

```java
int binarySearch(List list, Object key)//对List进行二分查找，返回索引，注意List必须是有序的
int max(Collection coll)//根据元素的自然顺序，返回最大的元素。 类比int min(Collection coll)
int max(Collection coll, Comparator c)//根据定制排序，返回最大元素，排序规则由Comparatator类控制。类比int min(Collection coll, Comparator c)
void fill(List list, Object obj)//用指定的元素代替指定list中的所有元素。
int frequency(Collection c, Object o)//统计元素出现次数
int indexOfSubList(List list, List target)//统计target在list中第一次出现的索引，找不到则返回-1，类比int lastIndexOfSubList(List source, list target).
boolean replaceAll(List list, Object oldVal, Object newVal), 用新元素替换旧元素
```

#### 5.3. 同步控制

`Collections` 提供了多个`synchronizedXxx()`方法·，该方法可以将指定集合包装成线程同步的集合，从而解决多线程并发访问集合时的线程安全问题。

我们知道 `HashSet`，`TreeSet`，`ArrayList`,`LinkedList`,`HashMap`,`TreeMap` 都是线程不安全的。`Collections` 提供了多个静态方法可以把他们包装成线程同步的集合。

最好不要用下面这些方法，效率非常低，需要线程安全的集合类型时请考虑使用 JUC 包下的并发集合。

方法如下：

```java
synchronizedCollection(Collection<T>  c) //返回指定 collection 支持的同步（线程安全的）collection。
synchronizedList(List<T> list)//返回指定列表支持的同步（线程安全的）List。
synchronizedMap(Map<K,V> m) //返回由指定映射支持的同步（线程安全的）Map。
synchronizedSet(Set<T> s) //返回指定 set 支持的同步（线程安全的）set。
```

#### 5.4. 设置不可变集合

Collections还可以设置不可变集合，提供了如下三类方法：

```java
//返回一个空的、不可变的集合对象，此处的集合既可以是List，也可以是Set，还可以是Map。
emptyXxx()

// 返回一个只包含指定对象（只有一个或一个元素）的不可变的集合对象，此处的集合可以是：List，Set，Map。
//不可变指集合里面的元素不可变(新增、修改、删除)
singletonXxx()

//返回指定集合对象的不可变视图，此处的集合可以是：List，Set，Map。
unmodifiableXxx()
```
上面三类方法的参数是原有的集合对象，返回值是该集合的”只读“版本。

### 6. Arrays类

##### 6.1. 常见操作

- 排序 : `sort()`  `parallelSort`
- 查找 : `binarySearch()`
- 比较: `equals()`
- 填充 : `fill()`
- 转列表:  `asList()`
- 转字符串 : `toString()`
- 复制: `copyOf()`

1、`sort()`

```java
		// *************排序 sort****************
		int a[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		// sort(int[] a)方法按照数字升序顺序排列指定的数组。
		Arrays.sort(a);
		System.out.println("Arrays.sort(a):");
		for (int i : a) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		// sort(int[] a,int fromIndex,int toIndex)按升序排列数组的指定范围
		int b[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		Arrays.sort(b, 2, 6);
		System.out.println("Arrays.sort(b, 2, 6):");
		for (int i : b) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int c[] = { 1, 3, 2, 7, 6, 5, 4, 9 };
		// parallelSort(int[] a) 按照数字顺序排列指定的数组(并行的)。同sort方法一样也有按范围的排序
		Arrays.parallelSort(c);
		System.out.println("Arrays.parallelSort(c)：");
		for (int i : c) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		// parallelSort给字符数组排序，sort也可以
		char d[] = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		Arrays.parallelSort(d);
		System.out.println("Arrays.parallelSort(d)：");
		for (char d2 : d) {
			System.out.print(d2);
		}
		// 换行
		System.out.println();

```

在做算法面试题的时候，我们还可能会经常遇到对字符串排序的情况,`Arrays.sort()` 对每个字符串的特定位置进行比较，然后按照升序排序。

```java
String[] strs = { "abcdehg", "abcdefg", "abcdeag" };
Arrays.sort(strs);
System.out.println(Arrays.toString(strs));//[abcdeag, abcdefg, abcdehg]
```

2、查找 : `binarySearch()`

binarySearch(): 排序后再进行二分查找，否则找不到
```java
		// *************查找 binarySearch()****************
		char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		// 排序后再进行二分查找，否则找不到
		Arrays.sort(e);
		System.out.println("Arrays.sort(e)" + Arrays.toString(e));
		System.out.println("Arrays.binarySearch(e, 'c')：");
		int s = Arrays.binarySearch(e, 'c');
		System.out.println("字符c在数组的位置：" + s);
```

3、比较: `equals()`

```java
		// *************比较 equals****************
		char[] e = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		char[] f = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		/*
		* 元素数量相同，并且相同位置的元素相同。 另外，如果两个数组引用都是null，则它们被认为是相等的 。
		*/
		// 输出true
		System.out.println("Arrays.equals(e, f):" + Arrays.equals(e, f));
```

4、填充 : `fill()`

```java
		// *************填充fill(批量初始化)****************
		int[] g = { 1, 2, 3, 3, 3, 3, 6, 6, 6 };
		// 数组中所有元素重新分配值
		Arrays.fill(g, 3);
		System.out.println("Arrays.fill(g, 3)：");
		// 输出结果：333333333
		for (int i : g) {
			System.out.print(i);
		}
		// 换行
		System.out.println();

		int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		// 数组中指定范围元素重新分配值  范围[start,end)
		Arrays.fill(h, 0, 2, 9);  
		System.out.println("Arrays.fill(h, 0, 2, 9);：");
		// 输出结果：993333666
		for (int i : h) {
			System.out.print(i);
		}
```

5、转列表 `asList()`

```java
		// *************转列表 asList()****************
		/*
		 * 返回由指定数组支持的固定大小的列表。
		 * （将返回的列表更改为“写入数组”。）该方法作为基于数组和基于集合的API之间的桥梁，与Collection.toArray()相结合 。
		 * 返回的列表是可序列化的，并实现RandomAccess 。
		 * 此方法还提供了一种方便的方式来创建一个初始化为包含几个元素的固定大小的列表如下：
		 */
		List<String> stooges = Arrays.asList("Larry", "Moe", "Curly");
		System.out.println(stooges);
```

5、转字符串 `toString()`

```java
		// *************转字符串 toString()****************
		/*
		* 返回指定数组的内容的字符串表示形式。
		*/
		char[] k = { 'a', 'f', 'b', 'c', 'e', 'A', 'C', 'B' };
		System.out.println(Arrays.toString(k));// [a, f, b, c, e, A, C, B]
```

6、复制 `copyOf()`

```java
		// *************复制 copy****************
		// copyOf 方法实现数组复制,h为数组，6为复制的长度
		int[] h = { 1, 2, 3, 3, 3, 3, 6, 6, 6, };
		int i[] = Arrays.copyOf(h, 6);
		System.out.println("Arrays.copyOf(h, 6);：");
		// 输出结果：123333
		for (int j : i) {
			System.out.print(j);
		}
		// 换行
		System.out.println();
		// copyOfRange将指定数组的指定范围复制到新数组中 范围[start,end)
		int j[] = Arrays.copyOfRange(h, 6, 11);
		System.out.println("Arrays.copyOfRange(h, 6, 11)："); 
		// 输出结果66600(h数组只有9个元素这里是从索引6到索引11复制所以不足的就为0)
		for (int j2 : j) {
			System.out.print(j2);
		}
		// 换行
		System.out.println();
```

### 7. 集合使用遇到的问题

#### 7.1. Collection.toArray()的使用

Collection.toArray()方法使用的坑以及如何反转数组？

Collection.toArray()该方法是一个泛型方法：`<T> T[] toArray(T[] a);` 如果`toArray`方法中没有传递任何参数的话返回的是`Object`类型数组。

> `Collection`而不是`Collections`,对应到具体的某一集合对象

```java
String [] s= new String[]{
    "dog", "lazy", "a", "over", "jumps", "fox", "brown", "quick", "A"
};
List<String> list = Arrays.asList(s);
Collections.reverse(list);
s=list.toArray(new String[0]);//没有指定类型的话默认为object[]数组，而不是String[],会报错
```

由于JVM优化，`new String[0]`作为`Collection.toArray()`方法的参数现在使用更好，`new String[0]`就是起一个模板的作用，指定了返回数组的类型，0是为了节省空间，因为它只是为了说明返回的类型。详见：<https://shipilev.net/blog/2016/arrays-wisdom-ancients/>


#### 7.2. 快速失败(fail-fast)

快速失败(fail-fast) 是 Java 集合的一种错误检测机制。在使用迭代器对集合进行遍历的时候，我们在多线程下操作非安全失败(fail-safe)的集合类可能就会触发 fail-fast 机制，导致抛出 `ConcurrentModificationException` 异常。 另外，在单线程下，如果在遍历过程中对集合对象的内容进行了修改的话也会触发 fail-fast 机制。

> 注：增强 for 循环也是借助迭代器进行遍历。

举个例子：多线程下，如果线程 1 正在对集合进行遍历，此时线程 2 对集合进行修改（增加、删除、修改），或者线程 1 在遍历过程中对集合进行修改，都会导致线程 1 抛出 `ConcurrentModificationException` 异常。

为什么呢？

每当迭代器使用 `hashNext()`/`next()`遍历下一个元素之前，都会检测 `modCount` 变量是否为 `expectedModCount` 值，是的话就返回遍历；否则抛出异常，终止遍历。

如果我们在集合被遍历期间对其进行修改的话，就会改变 `modCount` 的值，进而导致 `modCount != expectedModCount` ，进而抛出 `ConcurrentModificationException` 异常。

> 注：通过 `Iterator` 的方法修改集合的话会修改到 `expectedModCount` 的值，所以不会抛出异常。

```java
final void checkForComodification() {
    if (modCount != expectedModCount)
        throw new ConcurrentModificationException();
}
```

好吧！相信大家已经搞懂了快速失败(fail-fast)机制以及它的原理。

我们再来趁热打铁，看一个阿里巴巴手册相关的规定：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115162433384.png" alt="image-20210115162433384" style="zoom:70%;" />


有了前面讲的基础，我们应该知道：使用 `Iterator` 提供的 `remove` 方法，可以修改到 `expectedModCount` 的值。所以，才不会再抛出`ConcurrentModificationException` 异常。

1、什么是安全失败(fail-safe)呢？

明白了快速失败(fail-fast)之后，安全失败(fail-safe)我们就很好理解了。

采用安全失败机制的集合容器，在遍历时不是直接在集合内容上访问的，而是先复制原有集合内容，在拷贝的集合上进行遍历。所以，在遍历过程中对原集合所作的修改并不能被迭代器检测到，故不会抛 `ConcurrentModificationException` 异常。

2、不要在 foreach 循环里进行元素的 remove/add 操作


如果要进行`remove`操作，可以调用迭代器的 `remove `方法而不是集合类的 remove 方法。因为如果列表在任何时间从创建迭代器之后，以任何方式除通过迭代器自身`remove/add`方法，迭代器都将抛出一个`ConcurrentModificationException`,这就是单线程状态下产生的 **fail-fast 机制**。


```java
for (String item:list) {
    System.out.println(item);
    if("fox".equals(item)) {
        list.remove(item);
    }
}
```

3、实现原理

ArrayList定义了modCount变量，涉及到修改数组元素的操作（扩容add、删除），该变量会进行递增。

在迭代刚开始的时候会将modCount进行保存，每次迭代的时候判断list对象里面的modCount是否相等，不相等说明在迭代的时候对list里面的元素进行了修改，便抛出异常
```java
private class Itr implements Iterator<E> {
    //迭代开始的时候将modCount保存到expectedModCount中
	int expectedModCount = modCount;
	
	//next()获取下一个元素
	public E next() {	
		checkForComodification();
		...
	
	}
	//判断当前list对象的modCount和最开始预期的expectedModCount是否一致，不一致则抛出ConcurrentModificationException异常，防止读的时候并发的修改
	final void checkForComodification() {
		if (modCount != expectedModCount)
			throw new ConcurrentModificationException();
	}
}
```

foreach遍历的时候会创建迭代器，每次调用迭代器的ArrayList$Itr.next()方法获取下一个元素。next()方法在获取下一个元素之前会进行`checkForComodification`判断。

modCount为迭代之前的修改次数，在创建迭代器时`modCount == expectedModCount`，在迭代的过程中如果通过非迭代器自身`remove/add`方法，则modCount会++,此时`modCount != expectedModCount`。迭代器都将抛出一个`ConcurrentModificationException`

> fail-fast 机制 ：单线程或多线程情况下对fail-fast集合修改都会抛出`ConcurrentModificationException`异常。多个线程对` fail-fast` 集合进行修改的时，可能会抛出`ConcurrentModificationException`，单线程下也会出现这种情况，上面已经提到过。

`java.util`包下面的所有的集合类都是fail-fast的，而`java.util.concurrent`包下面的所有的类都是fail-safe的。


#### 7.3. Arrays.asList()避坑

最近使用`Arrays.asList()`遇到了一些坑，然后在网上看到这篇文章：[Java Array to List Examples](http://javadevnotes.com/java-array-to-list-examples) 感觉挺不错的，但是还不是特别全面。所以，自己对于这块小知识点进行了简单的总结。

1、简介

`Arrays.asList()`在平时开发中还是比较常见的，我们可以使用它将一个数组转换为一个 List 集合。

```java
String[] myArray = { "Apple", "Banana", "Orange" }；
List<String> myList = Arrays.asList(myArray);
//上面两个语句等价于下面一条语句
List<String> myList = Arrays.asList("Apple","Banana", "Orange");
```

JDK 源码对于这个方法的说明：

```java
/**
 *返回由指定数组支持的固定大小的列表。此方法作为基于数组和基于集合的API之间的桥梁，与 Collection.toArray()结合使用。返回的List是可序列化并实现RandomAccess接口。
 */
public static <T> List<T> asList(T... a) {
    return new ArrayList<>(a);
}
```

2、《阿里巴巴 Java 开发手册》对其的描述

`Arrays.asList()`  将数组转换为集合后,底层其实还是数组，《阿里巴巴 Java 开发手册》对于这个方法有如下描述：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210115162638824.png" alt="image-20210115162638824" style="zoom:70%;" />

3、使用时的注意事项总结

传递的数组必须是对象数组，而不是基本类型。

`Arrays.asList()`是泛型方法，传入的对象必须是对象数组。

```java
int[] myArray = { 1, 2, 3 };
List myList = Arrays.asList(myArray);
System.out.println(myList.size());//1
System.out.println(myList.get(0));//数组地址值
System.out.println(myList.get(1));//报错：ArrayIndexOutOfBoundsException
int [] array=(int[]) myList.get(0);
System.out.println(array[0]);//1
```

当传入一个原生数据类型数组时，`Arrays.asList()` 的真正得到的参数就不是数组中的元素，而是数组对象本身！此时 List 的唯一元素就是这个数组，这也就解释了上面的代码。

我们使用包装类型数组就可以解决这个问题。

```java
Integer[] myArray = { 1, 2, 3 };
```

使用集合的修改方法:`add()`、`remove()`、`clear()`会抛出异常。

```java
List myList = Arrays.asList(1, 2, 3);
myList.add(4);//运行时报错：UnsupportedOperationException
myList.remove(1);//运行时报错：UnsupportedOperationException
myList.clear();//运行时报错：UnsupportedOperationException
```

`Arrays.asList()` 方法返回的并不是 `java.util.ArrayList` ，而是 `java.util.Arrays` 的一个内部类,这个内部类并没有实现集合的修改方法或者说并没有重写这些方法。

```java
List myList = Arrays.asList(1, 2, 3);
System.out.println(myList.getClass());//class java.util.Arrays$ArrayList
```

下图是`java.util.Arrays$ArrayList`的简易源码，我们可以看到这个类重写的方法有哪些。

```java
  private static class ArrayList<E> extends AbstractList<E>
        implements RandomAccess, java.io.Serializable
    {
        ...

        @Override
        public E get(int index) {
          ...
        }

        @Override
        public E set(int index, E element) {
          ...
        }

        @Override
        public int indexOf(Object o) {
          ...
        }

        @Override
        public boolean contains(Object o) {
           ...
        }

        @Override
        public void forEach(Consumer<? super E> action) {
          ...
        }

        @Override
        public void replaceAll(UnaryOperator<E> operator) {
          ...
        }

        @Override
        public void sort(Comparator<? super E> c) {
          ...
        }
    }
```

我们再看一下`java.util.AbstractList`的`remove()`方法，这样我们就明白为啥会抛出`UnsupportedOperationException`。

```java
public E remove(int index) {
    throw new UnsupportedOperationException();
}
```

## 3-Java泛型

### 3.1. 泛型使用

Java 泛型（generics）是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许程序员在编译时检测到非法的类型。泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

> Java的泛型是伪泛型，这是因为Java在编译期间，所有的泛型信息都会被擦掉，这也就是通常所说类型擦除 。

```java
List<Integer> list = new ArrayList<>();

list.add(12);
//这里直接添加会报错
list.add("a");
Class<? extends List> clazz = list.getClass();
Method add = clazz.getDeclaredMethod("add", Object.class);
//但是通过反射添加，是可以的
add.invoke(list, "kl");

System.out.println(list)
```

1、泛型一般有三种使用方式: 泛型类、泛型接口、泛型方法。

- 泛型类：

```java
//此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
//在实例化泛型类时，必须指定T的具体类型
public class Generic<T>{ 
   
    private T key;

    public Generic(T key) { 
        this.key = key;
    }

    public T getKey(){ 
        return key;
    }
}
//实例化泛型类
Generic<Integer> genericInteger = new Generic<Integer>(123456);
```

- 泛型接口：

```java
public interface Generator<T> {
    public T method();
}
```

```java
//实现泛型接口，不指定类型
class GeneratorImpl<T> implements Generator<T>{
    @Override
    public T method() {
        return null;
    }
}
```

```java
//实现泛型接口，指定类型
class GeneratorImpl<T> implements Generator<String>{
    @Override
    public String method() {
        return "hello";
    }
}
```

- 泛型方法：
  - 方法泛型声明在返回值以及方法修饰符之间，使用`<>`进行声明 public static <T> T add(T x,T y)
  - 参数使用的时候不加`<>`  (T x,T y)

```java
public class Test {  
    public static void main(String[] args) {  
        /**不指定泛型的时候*/  
        int i = Test.add(1, 2); //这两个参数都是Integer，所以T为Integer类型  
        Number f = Test.add(1, 1.2); //这两个参数一个是Integer，一个是Float，所以取同一父类的最小级，为Number  
        Object o = Test.add(1, "asd"); //这两个参数一个是Integer，一个是Float，所以取同一父类的最小级，为Object  
        /**指定泛型的时候*/  
        int a = Test.<Integer>add(1, 2); //指定了Integer，所以只能为Integer类型或者其子类  
        int b = Test.<Integer>add(1, 2.2); //编译错误，指定了Integer，不能为Float  
        Number c = Test.<Number>add(1, 2.2); //指定为Number，所以可以为Integer和Float  
    }  

    //这是一个简单的泛型方法  
    public static <T> T add(T x,T y){  
        return y;  
    }  
}
```

2、常用的通配符为： T，E，K，V，？

- ？ 表示不确定的 java 类型
- T (type) 表示具体的一个java类型
- K V (key value) 分别代表java键值中的Key Value
- E (element) 代表Element

### 3.2. 类型擦除

大家都知道，Java的泛型是伪泛型，这是因为Java在编译期间，所有的泛型信息都会被擦掉，正确理解泛型概念的首要前提是理解`类型擦除`。Java的泛型基本上都是在编译器这个层次上实现的，在生成的字节码中是不包含泛型中的类型信息的，使用泛型的时候加上类型参数，在编译器编译的时候会去掉，这个过程成为类型擦除。

如在代码中定义 `List<Object>` 和 `List<String>` 等类型，在编译后都会变成`List`，JVM看到的只是`List`，而由泛型附加的类型信息对JVM是看不到的。Java编译器会在编译时尽可能的发现可能出错的地方，但是仍然无法在运行时刻出现的类型转换异常的情况，类型擦除也是Java的泛型与C++模板机制实现方式之间的重要区别。

#### 1. 通过两个例子证明Java类型的类型擦除

例1.原始类型相等

```java
public class Test {
    public static void main(String[] args) {
        ArrayList<String> list1 = new ArrayList<String>();
        list1.add("abc");
        ArrayList<Integer> list2 = new ArrayList<Integer>();
        list2.add(123);
        System.out.println(list1.getClass() == list2.getClass());
    }
}
```
- 在这个例子中，我们定义了两个`ArrayList`数组，不过一个是`ArrayList<String>`泛型类型的，只能存储字符串；一个是`ArrayList<Integer>`泛型类型的，只能存储整数
- 最后，我们通过list1对象和list2对象的getClass()方法获取他们的类的信息，最后发现结果为 `true`。说明泛型类型String和Integer都被擦除掉了，只剩下原始类型。


例2.通过反射添加其它类型元素

```java
public class Test {
   public static void main(String[] args) throws Exception{
        ArrayList<Integer> list = new ArrayList<Integer>();
        list.add(1);  //这样调用 add 方法只能存储整型数据，因为泛型类型的实例为 Integer
        Method method = list.getClass().getMethod("add", Object.class);
        method.invoke(list, "asd");
        for (int i = 0; i < list.size(); i++) {
            System.out.println(list.get(i));
        }
    }
}
```

- 在程序中定义了一个`ArrayList` 泛型类型实例化为`Integer`对象，如果直接调用`add()`方法，那么只能存储整数数据
- 当我们利用反射调用`add()`方法的时候，却可以存储字符串，这说明了`Integer`泛型实例在编译之后被擦除掉了，只保留了原始类型。

#### 2. 类型擦除后保留的原始类型

在上面，两次提到了原始类型，什么是原始类型？

- 原始类型： 就是擦除去了泛型信息，最后在字节码中的类型变量的真正类型，无论何时定义一个泛型，相应的原始类型都会被自动提供，类型变量擦除，并使用其限定类型（无限定的变量用Object）替换。

1、原始类型Object

```java
class Pair<T> {  
    private T value;  
    public T getValue() {  
        return value;  
    }  
    public void setValue(T  value) {  
        this.value = value;  
    }  
}  
```

Pair的原始类型为:
```java
class Pair {  
    private Object value;  
    public Object getValue() {  
        return value;  
    }  
    public void setValue(Object  value) {  
        this.value = value;  
    }  
}
```

因为在`Pair<T>`中，`T` 是一个无限定的类型变量，所以用`Object`替换，其结果就是一个普通的类，如同泛型加入Java语言之前的已经实现的样子。在程序中可以包含不同类型的`Pair`，如`Pair<String>`或`Pair<Integer>`，但是擦除类型后他们的就成为原始的`Pair`类型了，原始类型都是`Object`。

从上面的例2中，我们也可以明白`ArrayList<Integer>`被擦除类型后，原始类型也变为`Object`，所以通过反射我们就可以存储字符串了。

2、如果类型变量有限定，那么原始类型就用第一个边界的类型变量类替换。

比如: Pair这样声明的话
```java
public class Pair<T extends Comparable> {}
```
那么原始类型就是`Comparable`。要区分原始类型和泛型变量的类型。

3、在调用泛型方法时，可以指定泛型，也可以不指定泛型。

* 在不指定泛型的情况下，泛型变量的类型为该方法中的几种类型的同一父类的最小级，直到Object
* 在指定泛型的情况下，该方法的几种类型必须是该泛型的实例的类型或者其子类

```java
public class Test {  
    public static void main(String[] args) {  
        /**不指定泛型的时候*/  
        int i = Test.add(1, 2); //这两个参数都是Integer，所以T为Integer类型  
        Number f = Test.add(1, 1.2); //这两个参数一个是Integer，一个是Float，所以取同一父类的最小级，为Number  
        Object o = Test.add(1, "asd"); //这两个参数一个是Integer，一个是Float，所以取同一父类的最小级，为Object  
        /**指定泛型的时候*/  
        int a = Test.<Integer>add(1, 2); //指定了Integer，所以只能为Integer类型或者其子类  
        int b = Test.<Integer>add(1, 2.2); //编译错误，指定了Integer，不能为Float  
        Number c = Test.<Number>add(1, 2.2); //指定为Number，所以可以为Integer和Float  
    }  

    //这是一个简单的泛型方法  
    public static <T> T add(T x,T y){  
        return y;  
    }  
}
```

其实在泛型类中，不指定泛型的时候，也差不多，只不过这个时候的泛型为`Object`，就比如`ArrayList`中，如果不指定泛型，那么这个`ArrayList`可以存储任意的对象。

例4.Object泛型

```java
public static void main(String[] args) {  
    ArrayList list = new ArrayList();  
    list.add(1);  
    list.add("121");  
    list.add(new Date());  
}
```


#### 3. 类型擦除引起的问题及解决方法


因为种种原因，Java不能实现真正的泛型，只能使用类型擦除来实现伪泛型，这样虽然不会有类型膨胀问题，但是也引起来许多新问题，所以，SUN对这些问题做出了种种限制，避免我们发生各种错误。

先检查，再编译以及编译的对象和引用传递问题

Q: 既然说类型变量会在编译的时候擦除掉，那为什么我们往 ArrayList 创建的对象中添加整数会报错呢？不是说泛型变量String会在编译的时候变为Object类型吗？为什么不能存别的类型呢？既然类型擦除了，如何保证我们只能使用泛型变量限定的类型呢？

A: Java编译器是通过先检查代码中泛型的类型，然后在进行类型擦除，再进行编译。


例如：
```java
public static  void main(String[] args) {  
    ArrayList<String> list = new ArrayList<String>();  
    list.add("123");  
    list.add(123);//编译错误  
}
```

在上面的程序中，使用`add`方法添加一个整型，在IDE中，直接会报错，说明这就是在编译之前的检查，因为如果是在编译之后检查，类型擦除后，原始类型为`Object`，是应该允许任意引用类型添加的。可实际上却不是这样的，这恰恰说明了关于泛型变量的使用，是会在编译之前检查的。

#### 4. 类型检查检查的是引用

那么，这个类型检查是针对谁的呢？我们先看看参数化类型和原始类型的兼容。

以 ArrayList举例子，以前的写法:
```java
ArrayList list = new ArrayList();
```

现在的写法:
```java
ArrayList<String> list = new ArrayList<String>();
```
如果是与以前的代码兼容，各种引用传值之间，必然会出现如下的情况：

```java
ArrayList<String> list1 = new ArrayList(); //第一种 情况
ArrayList list2 = new ArrayList<String>(); //第二种 情况
```
这样是没有错误的，不过会有个编译时警告。在第一种情况，可以实现与完全使用泛型参数一样的效果，第二种则没有效果。

因为类型检查就是编译时完成的，new ArrayList()只是在内存中开辟了一个存储空间，可以存储任何类型对象，而真正涉及类型检查的是它的引用，因为我们是使用它引用list1来调用它的方法，比如说调用add方法，所以list1引用能完成泛型类型的检查。而引用list2没有使用泛型，所以不行。


举例子：
```java
public class Test {  
    public static void main(String[] args) {  
        ArrayList<String> list1 = new ArrayList();  
        list1.add("1"); //编译通过  
        list1.add(1); //编译错误  
        String str1 = list1.get(0); //返回类型就是String  

        ArrayList list2 = new ArrayList<String>();  
        list2.add("1"); //编译通过  
        list2.add(1); //编译通过  
        Object object = list2.get(0); //返回类型就是Object  
        
        new ArrayList<String>().add("11"); //编译通过  
        new ArrayList<String>().add(22); //编译错误  
        String str2 = new ArrayList<String>().get(0); //返回类型就是String  
    }  
}  
```

通过上面的例子，我们可以明白，类型检查就是针对引用的而不是针对new出来的对象，谁是一个引用，用这个引用调用泛型方法，就会对这个引用调用的方法进行类型检测，而无关它真正引用的对象。

#### 5. 参数化类型为什么不考虑继承关系？

泛型中参数化类型为什么不考虑继承关系？

在Java中，像下面形式的引用传递是不允许的:

```java
ArrayList<String> list1 = new ArrayList<Object>(); //编译错误  
ArrayList<Object> list2 = new ArrayList<String>(); //编译错误
```

我们先看第一种情况，将第一种情况拓展成下面的形式：

```java
ArrayList<Object> list1 = new ArrayList<Object>();  
list1.add(new Object());  
list1.add(new Object());  
ArrayList<String> list2 = list1; //编译错误
```

实际上，在第4行代码的时候，就会有编译错误。那么，我们先假设它编译没错。那么当我们使用list2引用用get()方法取值的时候，返回的都是`String`类型的对象（上面提到了，类型检测是根据引用来决定的），可是它里面实际上已经被我们存放了`Object`类型的对象，这样就会有`ClassCastException`了。所以为了避免这种极易出现的错误，Java不允许进行这样的引用传递。（这也是泛型出现的原因，就是为了解决类型转换的问题，我们不能违背它的初衷）


再看第二种情况，将第二种情况拓展成下面的形式：

```java
ArrayList<String> list1 = new ArrayList<String>();  
list1.add(new String());  
list1.add(new String());

ArrayList<Object> list2 = list1; //编译错误
```

这样的情况比第一种情况好的多，最起码，在我们用list2取值的时候不会出现`ClassCastException`，因为是从String转换为Object。可是，这样做有什么意义呢，泛型出现的原因，就是为了解决类型转换的问题。我们使用了泛型，到头来，还是要自己强转，违背了泛型设计的初衷。所以java不允许这么干。再说，你如果又用list2往里面add()新的对象，那么到时候取得时候，我怎么知道我取出来的到底是String类型的，还是Object类型的呢？

所以，要格外注意，泛型中的引用传递的问题。


#### 6. 自动类型转换

因为类型擦除的问题，所以所有的泛型类型变量最后都会被替换为原始类型。

既然都被替换为原始类型，那么为什么我们在获取的时候，不需要进行强制类型转换呢？

看下ArrayList.get()方法：

```java
public E get(int index) {  
    RangeCheck(index);  
    return (E) elementData[index];  
}
```

可以看到，在`return`之前，会根据泛型变量进行强转。假设泛型类型变量为`Date`，虽然泛型信息会被擦除掉，但是会将`(E) elementData[index]`，编译为`(Date)elementData[index]`。所以我们不用自己进行强转。

当存取一个泛型域时也会自动插入强制类型转换。假设`Pair`类的`value`域是`public`的，那么表达式：
```java
Date date = pair.value;
```
也会自动地在结果字节码中插入强制类型转换。

#### 7. 类型擦除与多态的冲突和解决方法

现在有这样一个泛型类：
```java
class Pair<T> {  
    private T value;  
    public T getValue() {  
        return value;  
    }  
    public void setValue(T value) {  
        this.value = value;  
    }  
}
```

然后我们想要一个子类继承它。
```java
class DateInter extends Pair<Date> {  
    @Override  
    public void setValue(Date value) {  
        super.setValue(value);  
    }  
    @Override  
    public Date getValue() {  
        return super.getValue();  
    }  
}
```
在这个子类中，我们设定父类的泛型类型为`Pair<Date>`，在子类中，我们覆盖了父类的两个方法，我们的原意是这样的：将父类的泛型类型限定为`Date`，那么父类里面的两个方法的参数都为 `Date` 类型。

```java
public Date getValue() {  
    return value;  
}  
public void setValue(Date value) {  
    this.value = value;  
}
```

所以，我们在子类中重写这两个方法一点问题也没有，实际上，从他们的`@Override`标签中也可以看到，一点问题也没有，实际上是这样的吗？

分析：实际上，类型擦除后，父类的的泛型类型全部变为了原始类型`Object`，所以父类编译之后会变成下面的样子：

```java
class Pair {  
    private Object value;  
    public Object getValue() {  
        return value;  
    }  
    public void setValue(Object  value) {  
        this.value = value;  
    }  
}
```

再看子类的两个重写的方法的类型：

```java
@Override  
public void setValue(Date value) {  
    super.setValue(value);  
}  
@Override  
public Date getValue() {  
    return super.getValue();  
}
```
先来分析`setValue`方法，父类的类型是`Object`，而子类的类型是`Date`，参数类型不一样，这如果实在普通的继承关系中，根本就不会是重写，而是重载。


我们在一个main方法测试一下：
```java
public static void main(String[] args) throws ClassNotFoundException {  
        DateInter dateInter = new DateInter();  
        dateInter.setValue(new Date());                  
        dateInter.setValue(new Object()); //编译错误  
}
```

如果是重载，那么子类中两个`setValue`方法，一个是参数`Object`类型，一个是`Date`类型，可是我们发现，根本就没有这样的一个子类继承自父类的Object类型参数的方法。所以说，确实是重写了，而不是重载了。

为什么会这样呢？

原因是这样的，我们传入父类的泛型类型是`Date`，`Pair<Date>`，我们的本意是将泛型类变为如下：

```java
class Pair {  
    private Date value;  
    public Date getValue() {  
        return value;  
    }  
    public void setValue(Date value) {  
        this.value = value;  
    }  
}
```
然后在子类中重写参数类型为`Date`的那两个方法，实现继承中的多态。

可是由于种种原因，虚拟机并不能将泛型类型变为`Date`，只能将类型擦除掉，变为原始类型`Object`。这样，我们的本意是进行重写，实现多态。可是类型擦除后，只能变为了重载。这样，类型擦除就和多态有了冲突（由重写变为了重载）。JVM知道你的本意吗？知道！！！可是它能直接实现吗，不能！！！如果真的不能的话，那我们怎么去重写我们想要的`Date`类型参数的方法啊。

于是JVM采用了一个特殊的方法，来完成这项功能，那就是桥方法。

首先，我们用 `javap -c className` 的方式反编译下`DateInter`子类的字节码，结果如下：

```java
class com.tao.test.DateInter extends com.tao.test.Pair<java.util.Date> {  
  com.tao.test.DateInter();  
    Code:  
       0: aload_0  
       1: invokespecial #8                  // Method com/tao/test/Pair."<init>":()V  
       4: return  

  public void setValue(java.util.Date);  //我们重写的setValue方法  
    Code:  
       0: aload_0  
       1: aload_1  
       2: invokespecial #16                 // Method com/tao/test/Pair.setValue:(Ljava/lang/Object;)V  
       5: return  

  public java.util.Date getValue();    //我们重写的getValue方法  
    Code:  
       0: aload_0  
       1: invokespecial #23                 // Method com/tao/test/Pair.getValue:()Ljava/lang/Object;  
       4: checkcast     #26                 // class java/util/Date  
       7: areturn  

  public java.lang.Object getValue();     //编译时由编译器生成的桥方法  
    Code:  
       0: aload_0  
       1: invokevirtual #28                 // Method getValue:()Ljava/util/Date 去调用我们重写的getValue方法;  
       4: areturn  

  public void setValue(java.lang.Object);   //编译时由编译器生成的桥方法  
    Code:  
       0: aload_0  
       1: aload_1  
       2: checkcast     #26                 // class java/util/Date  
       5: invokevirtual #30                 // Method setValue:(Ljava/util/Date; 去调用我们重写的setValue方法)V  
       8: return  
}
```

从编译的结果来看，我们本意重写`setValue`和`getValue`方法的子类，竟然有4个方法，其实不用惊奇，最后的两个方法，就是编译器自己生成的桥方法。可以看到桥方法的参数类型都是 `Object`，也就是说，子类中真正覆盖父类两个方法的就是这两个我们看不到的桥方法。而打在我们自己定义的 `setValue` 和 `getValue` 方法上面的 `@Override` 只不过是假象。而桥方法的内部实现，就只是去调用我们自己重写的那两个方法。

所以，虚拟机巧妙的使用了桥方法，来解决了类型擦除和多态的冲突。

不过，要提到一点，这里面的 `setValue`  和 `getValue`  这两个桥方法的意义又有不同。

`setValue` 方法是为了解决类型擦除与多态之间的冲突。

而 `getValue` 却有普遍的意义，怎么说呢，如果这是一个普通的继承关系：

那么父类的`setValue`方法如下：
```java
public Object getValue() {  
    return super.getValue();  
}
```

而子类重写的方法是：
```java
public Date getValue() {  
    return super.getValue();  
}
```

其实这在普通的类继承中也是普遍存在的重写，这就是 **协变**。

并且，还有一点也许会有疑问，子类中的桥方法 `Object getValue()`  和`Date getValue()` 是同时存在的，可是如果是常规的两个方法，他们的方法签名是一样的，也就是说虚拟机根本不能分别这两个方法。如果是我们自己编写Java代码，这样的代码是无法通过编译器的检查的，但是虚拟机却是允许这样做的，因为虚拟机通过参数类型和返回类型来确定一个方法，所以编译器为了实现泛型的多态允许自己做这个看起来“不合法”的事情，然后交给虚拟器去区别。

#### 8. 泛型类型变量不能是基本数据类型

不能用类型参数替换基本类型。就比如，没有`ArrayList<double>`，只有`ArrayList<Double>`。因为当类型擦除后，`ArrayList`的原始类型变为`Object`，但是`Object`类型不能存储`double`值，只能引用`Double`的值。


#### 9. 编译时集合的 `instanceof`

```java
ArrayList<String> arrayList = new ArrayList<String>();
```

因为类型擦除之后，`ArrayList<String>`只剩下原始类型，泛型信息`String`不存在了。那么，编译时进行类型查询的时候使用下面的方法是错误的

```java
if( arrayList instanceof ArrayList<String>)
```


#### 10. 泛型在静态方法和静态类中的问题

泛型类中的静态方法和静态变量不可以使用泛型类所声明的泛型类型参数，但可以单独去在方法上进行声明


举例说明：
```java
public class Test2<T> {    
    public static T one;   //编译错误    
    public static  T show(T one){ //编译错误    
        return null;    
    }    
}
```

因为泛型类中的泛型参数的实例化是在定义对象的时候指定的，而静态变量和静态方法不需要使用对象来调用。对象都没有创建，如何确定这个泛型参数是何种类型，所以当然是错误的。

但是要注意区分下面的一种情况：
```java
public class Test2 {    
    public static <T> T show(T one){ //这是正确的    
        return null;    
    }    
}
```

单独在show静态方法上声明了泛型参数。

### 3.3.泛型中的通配符

1、前言

Java 泛型（generics）是 JDK 5 中引入的一个新特性, 泛型提供了编译时类型安全检测机制，该机制允许开发者在编译时检测到非法的类型。

泛型的本质是参数化类型，也就是说所操作的数据类型被指定为一个参数。

2、泛型带来的好处


在没有泛型的情况的下，通过对类型 Object 的引用来实现参数的“任意化”，“任意化”带来的缺点是要做显式的强制类型转换，而这种转换是要求开发者对实际参数类型可以预知的情况下进行的。对于强制类型转换错误的情况，编译器可能不提示错误，在运行的时候才出现异常，这是本身就是一个安全隐患。


那么泛型的好处就是**在编译的时候能够检查类型安全，并且所有的强制转换都是自动和隐式的**

```java
public class GlmapperGeneric<T> {
	private T t;
    public void set(T t) { this.t = t; }
    public T get() { return t; }
  
    public static void main(String[] args) {
        // do nothing
    }

  /**
    * 不指定类型
    */
  public void noSpecifyType(){
    GlmapperGeneric glmapperGeneric = new GlmapperGeneric();
    glmapperGeneric.set("test");
    // 需要强制类型转换
    String test = (String) glmapperGeneric.get();
    System.out.println(test);
  }

  /**
    * 指定类型
    */
  public void specifyType(){
    GlmapperGeneric<String> glmapperGeneric = new GlmapperGeneric();
    glmapperGeneric.set("test");
    // 不需要强制类型转换
    String test = glmapperGeneric.get();
    System.out.println(test);
  }
}

```

上面这段代码中的` specifyType` 方法中 省去了强制转换，可以在编译时候检查类型安全，可以用在类，方法，接口上。

我们在定义泛型类，泛型方法，泛型接口的时候经常会碰见很多不同的通配符，比如 T，E，K，V 等等，这些通配符又都是什么意思呢？


#### 1. 常用的 T，E，K，V，？


本质上这些个都是通配符，没啥区别，只不过是编码时的一种约定俗成的东西。比如上述代码中的 T ，我们可以换成 A-Z 之间的任何一个 字母都可以，并不会影响程序的正常运行，但是如果换成其他的字母代替 T ，在可读性上可能会弱一些。通常情况下，T，E，K，V，？ 是这样约定的：

* ？ 表示不确定的 java 类型
* T (type) 表示具体的一个java类型
* K V (key value) 分别代表java键值中的Key Value
* E (element) 代表Element


#### 2. `？` 无界通配符

我有一个父类 Animal 和几个子类，如狗、猫等，现在我需要一个动物的列表，我的第一个想法是像这样的：

```java
List<Animal> listAnimals
```

但是老板的想法确实这样的：

```java
List<? extends Animal> listAnimals
```

为什么要使用通配符而不是简单的泛型呢？通配符其实在声明局部变量时是没有什么意义的，但是当你为一个方法声明一个参数时，它是非常重要的。
```java
static int countLegs (List<? extends Animal > animals ) {
    int retVal = 0;
    for ( Animal animal : animals )
    {
        retVal += animal.countLegs();
    }
    return retVal;
}

static int countLegs1 (List< Animal > animals ){
    int retVal = 0;
    for ( Animal animal : animals )
    {
        retVal += animal.countLegs();
    }
    return retVal;
}

public static void main(String[] args) {
    List<Dog> dogs = new ArrayList<>();
 	// 不会报错
    countLegs( dogs );
	// 报错
    countLegs1(dogs);
}

```

当调用 countLegs1 时，就会飘红，提示的错误信息如下：
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210118172652213.png" alt="image-20210118172652213" style="zoom:60%;" />

所以，对于不确定或者不关心实际要操作的类型，可以使用无限制通配符（尖括号里一个问号，即 <?> ），表示可以持有任何类型。像 countLegs 方法中，限定了上界为Animal，但是不关心具体类型是什么，所以对于传入的 Animal 的所有子类都可以支持，并且不会报错。而 countLegs1 就不行。


#### 3. 上界通配符 `< ? extends E>`

上界：用 `extends` 关键字声明，表示参数化的类型可能是所指定的类型，或者是此类型的子类。

>参数化类型不考虑继承关系，可以使用上界通配符指定泛型，表示参数化的类型可能是所指定的类型，或者是此类型的子类

在类型参数中使用 extends 表示这个泛型中的参数必须是 E 或者 E 的子类，这样有两个好处：

* 如果传入的类型不是 E 或者 E 的子类，编译不成功
* 泛型中可以使用 E 的方法，要不然还得强转成 E 才能使用

```java
private <K extends A, E extends B> E test(K arg1, E arg2){
    E result = arg2;
    arg2.compareTo(arg1);
    //.....
    return result;
}
```

>类型参数列表中如果有多个类型参数上限，用逗号分开


#### 4. 下界通配符 `< ? super E>`

>下界: 用 super 进行声明，表示参数化的类型可能是所指定的类型，或者是此类型的父类型，直至 Object

在类型参数中使用 super 表示这个泛型中的参数必须是 E 或者 E 的父类。

```java
private <T> void test(List<? super T> dst, List<T> src){
    for (T t : src) {
        dst.add(t);
    }
}

public static void main(String[] args) {
    List<Dog> dogs = new ArrayList<>();
    List<Animal> animals = new ArrayList<>();
    new Test3().test(animals,dogs);
}

// Dog 是 Animal 的子类
class Dog extends Animal {

}
```

dst 类型 “大于等于” src 的类型，这里的“大于等于”是指 dst 表示的范围比 src 要大，因此装得下 dst 的容器也就能装 src 。


#### 5. `？` 和 `T` 的区别

？和 T 都表示不确定的类型，T表示不确定的某一类型，而 ? 表示不确定的任意类型。

* 区别在于我们可以对 T 进行操作，但是对 ？不行，比如如下这种 ：

```java
// 可以
T t = operate();

// 不可以
？ car = operate();
```

简单总结下：

T 是一个 `确定的`  某一类型，通常用于**泛型类和泛型方法的定义**，？是一个 `不确定`  的类型，通常用于泛型方法的调用代码和形参，不能用于定义类和泛型方法。

1、区别1：通过 T 来确保泛型参数的一致性

```java
// 通过 T 来 确保 泛型参数的一致性
public <T extends Number> void test(List<T> dest, List<T> src)

//通配符是 不确定的，所以这个方法不能保证两个 List 具有相同的元素类型
public void test(List<? extends Number> dest, List<? extends Number> src)
```

不能保证两个 List 具有相同的元素类型的情况

```java
GlmapperGeneric<String> glmapperGeneric = new GlmapperGeneric<>();
List<String> dest = new ArrayList<>();
List<Number> src = new ArrayList<>();
glmapperGeneric.testNon(dest,src);
```

上面的代码在编译器并不会报错，但是当进入到 testNon 方法内部操作时（比如赋值），对于 dest 和 src 而言，就还是需要进行类型转换。

2、区别2：类型参数可以多重限定而通配符不行

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210118172818659.png" alt="image-20210118172818659" style="zoom:50%;" />

使用 `&` 符号设定多重边界（Multi Bounds)，指定泛型类型 T 必须是 `MultiLimitInterfaceA` 和 `MultiLimitInterfaceB` 的共有子类型，此时变量 t 就具有了所有限定的方法和属性。对于通配符来说，因为它不是一个确定的类型，所以不能进行多重限定。

3、区别3：通配符 ？可以使用超类限定而类型参数 T 不行

类型参数 T 只具有一种类型限定方式：

```java
T extends A
```

但是通配符 ? 可以进行 两种限定：

```java
? extends A
? super A
```


#### 6. `Class<T>` 和 `Class<?>` 区别

前面介绍了 ？ 和 T 的区别，那么对于，Class<T> 和 <Class<?> 又有什么区别呢？

最常见的是在反射场景下的使用，这里以用一段发射的代码来说明下。

```java
// 通过反射的方式生成  multiLimit 对象，这里比较明显的是，我们需要使用强制类型转换
MultiLimit multiLimit = (MultiLimit)Class.forName("com.glmapper.bridge.boot.generic.MultiLimit").newInstance();
```

对于上述代码，在运行期，如果反射的类型不是 `MultiLimit` 类，那么一定会报` java.lang.ClassCastException` 错误。

对于这种情况，则可以使用下面的代码来代替，使得在在编译期就能直接检查到类型的问题：
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210118172913040.png" alt="image-20210118172913040" style="zoom:66%;" />


Class<T> 在实例化的时候，T 要替换成具体类。Class<?> 它是个通配泛型，? 可以代表任何类型，所以主要用于声明时的限制情况。比如，我们可以这样做申明：
```java
// 可以
public Class<?> clazz;
// 不可以，因为 T 需要指定类型
public Class<T> clazzT;
```

所以当不知道声明什么类型的 Class 的时候可以定义一个Class<?>。
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210118172956134.png" alt="image-20210118172956134" style="zoom:70%;" />


那如果也想 `public Class<T> clazzT;` 这样的话，就必须让当前的类也指定 T 
```java
public class Test3<T> {
    public Class<?> clazz;
    // 不会报错
    public Class<T> clazzT;
```

## 4-Java枚举

### 4.1. 枚举概览

在本文中，我们将看到什么是 Java 枚举，它们解决了哪些问题以及如何在实践中使用 Java 枚举实现一些设计模式。

- enum关键字在 java5 中引入，表示一种特殊类型的类，其总是继承java.lang.Enum类，更多内容可以自行查看其[官方文档](https://docs.oracle.com/javase/6/docs/api/java/lang/Enum.html)。

- 枚举在很多时候会和常量拿来对比，可能因为本身我们大量实际使用枚举的地方就是为了替代常量。那么这种方式由什么优势呢？

- 以这种方式定义的常量使代码更具可读性，允许进行编译时检查，预先记录可接受值的列表，并避免由于传入无效值而引起的意外行为。


下面示例定义一个简单的枚举类型 pizza 订单的状态，共有三种 ORDERED, READY, DELIVERED状态:

```java
package shuang.kou.enumdemo.enumtest;

public enum PizzaStatus {
    ORDERED,
    READY, 
    DELIVERED; 
}
```

简单来说，我们通过上面的代码避免了定义常量，我们将所有和 pizza 订单的状态的常量都统一放到了一个枚举类型里面。

```java
System.out.println(PizzaStatus.ORDERED.name());//ORDERED
System.out.println(PizzaStatus.ORDERED);//ORDERED
System.out.println(PizzaStatus.ORDERED.name().getClass());//class java.lang.String
System.out.println(PizzaStatus.ORDERED.getClass());//class shuang.kou.enumdemo.enumtest.PizzaStatus
```
每一个枚举类型有 `name()` 方法获取当前枚举类型的名称


#### 1. 方法中使用枚举

现在我们对枚举是什么以及如何使用它们有了基本的了解，让我们通过定义一些额外的API方法, 在API方法中使用枚举，将上一个示例提升到一个新的水平：

```java
public class Pizza {
    private PizzaStatus status;
    public enum PizzaStatus {
        ORDERED,
        READY,
        DELIVERED;
    }
 
    public boolean isDeliverable() {
        if (getStatus() == PizzaStatus.READY) {
            return true;
        }
        return false;
    }
     
    // Methods that set and get the status variable.
}
```

#### 2. 使用 == 比较枚举类型

由于枚举类型确保JVM中仅存在一个常量实例，因此我们可以安全地使用“ ==”运算符比较两个变量，如上例所示；此外，“ ==”运算符可提供编译时和运行时的安全性。

首先，让我们看一下以下代码段中的运行时安全性，其中“ ==”运算符用于比较状态，并且如果两个值均为null 都不会引发 `NullPointerException`。相反，如果使用equals方法，将抛出 `NullPointerException`：

```java
if(testPz.getStatus().equals(Pizza.PizzaStatus.DELIVERED)); 
if(testPz.getStatus() == Pizza.PizzaStatus.DELIVERED); 
```

对于编译时安全性，我们看另一个示例，两个不同枚举类型进行比较，使用equal方法比较结果确定为true，因为getStatus方法的枚举值与另一个类型枚举值一致，但逻辑上应该为false。这个问题可以使用==操作符避免。因为编译器会表示类型不兼容错误：

```java
if(testPz.getStatus().equals(TestColor.GREEN));
if(testPz.getStatus() == TestColor.GREEN);
```

#### 3. 在 switch 语句中使用枚举类型

```java
public class Pizza {
    private PizzaStatus status;
    public enum PizzaStatus {
        ORDERED,
        READY,
        DELIVERED;
    }
    public int getDeliveryTimeInDays() {
        switch (status) {
            case ORDERED: return 5;
            case READY: return 2;
            case DELIVERED: return 0;
        }
        return 0;
    }
    // Methods that set and get the status variable.
}
```

### 4.2. 枚举类型的属性、方法、构造函数、实现接口

#### 1. 属性、方法和构造函数

你可以通过在枚举类型中定义属性、方法和构造函数让它变得更加强大。

- 构造方法：枚举构造方法必须是private，可以不写，默认为private。在枚举类型中，使用构造方法定义枚举类型实例 `枚举名称(构造参数...)` 可同时重写枚举类型定义的方法。

- 属性：枚举可以定义枚举实例的私有属性,并提供属性的getter和setter方法。

- 方法：定义枚举方法，定义枚举类型实例时可以重写定义的方法


```java
public enum PizzaStatus {
        ORDERED (5){
            @Override
            public boolean isOrdered() {
                return true;
            }
        },
        READY (2){
            @Override
            public boolean isReady() {
                return true;
            }
        },
        DELIVERED (0){
            @Override
            public boolean isDelivered() {
                return true;
            }
        };
 
        private int timeToDelivery;
 
        public boolean isOrdered() {return false;}
 
        public boolean isReady() {return false;}
 
        public boolean isDelivered(){return false;}
 
        public int getTimeToDelivery() {
            return timeToDelivery;
        }
 
        PizzaStatus (int timeToDelivery) {
            this.timeToDelivery = timeToDelivery;
        }
}
```

下面这段代码展示它是如何 work 的：

```java
System.out.println(PizzaStatus.ORDERED.isOrdered());//true
System.out.println(PizzaStatus.ORDERED.getTimeToDelivery());//5
```

#### 2. 实现接口

实现接口: 
```java
public enum ChnlResultCode implements IErrorCode {
    ...
}
```
在枚举里面重写接口方法。

#### 3. 使用例子


下面我通过一个实际的例子展示一下，当我们调用短信验证码的时候可能有几种不同的用途，我们在下面这样定义：

```java

public enum PinType {

    REGISTER(100000, "注册使用"),
    FORGET_PASSWORD(100001, "忘记密码使用"),
    UPDATE_PHONE_NUMBER(100002, "更新手机号码使用");

    private final int code;
    private final String message;

    PinType(int code, String message) {
        this.code = code;
        this.message = message;
    }

    public int getCode() {
        return code;
    }

    public String getMessage() {
        return message;
    }

    @Override
    public String toString() {
        return "PinType{" +
                "code=" + code +
                ", message='" + message + '\'' +
                '}';
    }
}
```

实际使用：

```java
System.out.println(PinType.FORGET_PASSWORD.getCode());
System.out.println(PinType.FORGET_PASSWORD.getMessage());
System.out.println(PinType.FORGET_PASSWORD.toString());
```

Output:

```java
100001
忘记密码使用
PinType{code=100001, message='忘记密码使用'}
```

这样的话，在实际使用起来就会非常灵活方便！

### 4.3. EnumSet and EnumMap

#### 1. EnumSet

`EnumSet` 是一种专门为枚举类型所设计的 `Set` 类型。

- 与`HashSet`相比，由于使用了内部位向量表示，因此它是特定 `Enum` 常量集的非常有效且紧凑的表示形式。

- 它提供了类型安全的替代方法，以替代传统的基于int的“位标志”，使我们能够编写更易读和易于维护的简洁代码。

- `EnumSet` 是抽象类，其有两个实现：`RegularEnumSet` 、`JumboEnumSet`，选择哪一个取决于实例化时枚举中常量的数量。

在很多场景中的枚举常量集合操作（如：取子集、增加、删除、`containsAll`和`removeAll`批操作）使用`EnumSet`非常合适；如果需要迭代所有可能的常量则使用`Enum.values()`。

```java
public class Pizza {
 
    private static EnumSet<PizzaStatus> undeliveredPizzaStatuses = EnumSet.of(PizzaStatus.ORDERED, PizzaStatus.READY);
 
    private PizzaStatus status;
 
    public enum PizzaStatus {
        ...
    }
 
    public boolean isDeliverable() {
        return this.status.isReady();
    }
 
    public void printTimeToDeliver() {
        System.out.println("Time to delivery is " + 
          this.getStatus().getTimeToDelivery() + " days");
    }
 
    public static List<Pizza> getAllUndeliveredPizzas(List<Pizza> input) {
        return input.stream().filter(
          (s) -> undeliveredPizzaStatuses.contains(s.getStatus()))
            .collect(Collectors.toList());
    }
 
    public void deliver() { 
        if (isDeliverable()) { 
            PizzaDeliverySystemConfiguration.getInstance().getDeliveryStrategy()
              .deliver(this); 
            this.setStatus(PizzaStatus.DELIVERED); 
        } 
    }
     
    // Methods that set and get the status variable.
}
```

  下面的测试演示了展示了 `EnumSet` 在某些场景下的强大功能：

```java
@Test
public void givenPizaOrders_whenRetrievingUnDeliveredPzs_thenCorrectlyRetrieved() {
    List<Pizza> pzList = new ArrayList<>();
    Pizza pz1 = new Pizza();
    pz1.setStatus(Pizza.PizzaStatus.DELIVERED);
 
    Pizza pz2 = new Pizza();
    pz2.setStatus(Pizza.PizzaStatus.ORDERED);
 
    Pizza pz3 = new Pizza();
    pz3.setStatus(Pizza.PizzaStatus.ORDERED);
 
    Pizza pz4 = new Pizza();
    pz4.setStatus(Pizza.PizzaStatus.READY);
 
    pzList.add(pz1);
    pzList.add(pz2);
    pzList.add(pz3);
    pzList.add(pz4);
 
    List<Pizza> undeliveredPzs = Pizza.getAllUndeliveredPizzas(pzList); 
    assertTrue(undeliveredPzs.size() == 3); 
}
```

#### 2. EnumMap

`EnumMap`是一个专门化的映射实现，用于将枚举常量用作键。与对应的 `HashMap` 相比，它是一个高效紧凑的实现，并且在内部表示为一个数组:

```java
EnumMap<Pizza.PizzaStatus, Pizza> map;
```

让我们快速看一个真实的示例，该示例演示如何在实践中使用它：

```java
public static EnumMap<PizzaStatus, List<Pizza>>  groupPizzaByStatus(List<Pizza> pizzaList) {
    EnumMap<PizzaStatus, List<Pizza>> pzByStatus =   new EnumMap<PizzaStatus, List<Pizza>>(PizzaStatus.class);
    for (Pizza pz : pizzaList) {
        PizzaStatus status = pz.getStatus();
        if (pzByStatus.containsKey(status)) {
            pzByStatus.get(status).add(pz);
        } else {
            List<Pizza> newPzList = new ArrayList<Pizza>();
            newPzList.add(pz);
            pzByStatus.put(status, newPzList);
        }
    }
    return pzByStatus;
}
```

 下面的测试演示了展示了 `EnumMap` 在某些场景下的强大功能：

```java
@Test
public void givenPizaOrders_whenGroupByStatusCalled_thenCorrectlyGrouped() {
    List<Pizza> pzList = new ArrayList<>();
    Pizza pz1 = new Pizza();
    pz1.setStatus(Pizza.PizzaStatus.DELIVERED);
 
    Pizza pz2 = new Pizza();
    pz2.setStatus(Pizza.PizzaStatus.ORDERED);
 
    Pizza pz3 = new Pizza();
    pz3.setStatus(Pizza.PizzaStatus.ORDERED);
 
    Pizza pz4 = new Pizza();
    pz4.setStatus(Pizza.PizzaStatus.READY);
 
    pzList.add(pz1);
    pzList.add(pz2);
    pzList.add(pz3);
    pzList.add(pz4);
 
    EnumMap<Pizza.PizzaStatus,List<Pizza>> map = Pizza.groupPizzaByStatus(pzList);
    assertTrue(map.get(Pizza.PizzaStatus.DELIVERED).size() == 1);
    assertTrue(map.get(Pizza.PizzaStatus.ORDERED).size() == 2);
    assertTrue(map.get(Pizza.PizzaStatus.READY).size() == 1);
}
```


#### 3. Java 8 重写

Pizza 类可以用Java 8重写，您可以看到方法 lambda 和Stream API如何使 `getAllUndeliveredPizzas（）`和`groupPizzaByStatus（）`方法变得如此简洁：

`getAllUndeliveredPizzas（）`:

```java
public static List<Pizza> getAllUndeliveredPizzas(List<Pizza> input) {
	return input.stream().filter((s) -> !undeliveredPizzaStatuses.contains(s.getStatus()))
			.collect(Collectors.toList());
}
```

`groupPizzaByStatus（）` :

```java
public static EnumMap<PizzaStatus, List<Pizza>> groupPizzaByStatus(List<Pizza> pzList) {
	EnumMap<PizzaStatus, List<Pizza>> map = pzList.stream().collect(
			Collectors.groupingBy(Pizza::getStatus,() -> new EnumMap<>(PizzaStatus.class), Collectors.toList()));
	return map;
}
```

### 4.4. 通过枚举实现一些设计模式

#### 1. 单例模式

通常，使用类实现 Singleton 模式并非易事，枚举提供了一种实现单例的简便方法。

《Effective Java 》和《Java与模式》都非常推荐这种方式，使用这种方式方式实现枚举可以有什么好处呢？

《Effective Java》

> 这种方法在功能上与公有域方法相近，但是它更加简洁，无偿提供了序列化机制，绝对防止多次实例化，即使是在面对复杂序列化或者反射攻击的时候。虽然这种方法还没有广泛采用，但是单元素的枚举类型已经成为实现 Singleton的最佳方法。 —-《Effective Java 中文版 第二版》

《Java与模式》

>  《Java与模式》中，作者这样写道，使用枚举来实现单实例控制会更加简洁，而且无偿地提供了序列化机制，并由JVM从根本上提供保障，绝对防止多次实例化，是更简洁、高效、安全的实现单例的方式。

下面的代码段显示了如何使用枚举实现单例模式：

```java
public enum PizzaDeliverySystemConfiguration {
    INSTANCE;
 
    /**
     * 枚举构造方法
     */
    PizzaDeliverySystemConfiguration() {
        // Initialization configuration which involves
        // overriding defaults like delivery strategy
    }
    /**
     * 获取单例
     * @return
     */
    public static PizzaDeliverySystemConfiguration getInstance() {
        return INSTANCE;
    }
    /**
     * 枚举实例的方法
     * @return
     */
    public PizzaDeliveryStrategy getDeliveryStrategy() {
        return deliveryStrategy;
    }
}
```

如何使用呢？请看下面的代码：

```java
PizzaDeliveryStrategy deliveryStrategy = PizzaDeliverySystemConfiguration.getInstance().getDeliveryStrategy();
```

通过 `PizzaDeliverySystemConfiguration.getInstance()` 获取的就是单例的 `PizzaDeliverySystemConfiguration`


#### 2. 策略模式

通常，策略模式由不同类实现同一个接口来实现的。这也就意味着添加新策略意味着添加新的实现类。使用枚举，可以轻松完成此任务，添加新的实现意味着只定义具有某个实现的另一个实例。

下面的代码段显示了如何使用枚举实现策略模式：

```java
public enum PizzaDeliveryStrategy {
    EXPRESS {
        @Override
        public void deliver(Pizza pz) {
            System.out.println("Pizza will be delivered in express mode");
        }
    },
    NORMAL {
        @Override
        public void deliver(Pizza pz) {
            System.out.println("Pizza will be delivered in normal mode");
        }
    };
 
    public abstract void deliver(Pizza pz);
}
```

定义新的枚举实例的时候，实现对应的抽象方法。


给 `Pizza `增加下面的方法：

```java
public void deliver() {
    if (isDeliverable()) {
        PizzaDeliverySystemConfiguration.getInstance().getDeliveryStrategy().deliver(this);
        this.setStatus(PizzaStatus.DELIVERED);
    }
}
```

如何使用呢？请看下面的代码：

```java
@Test
public void givenPizaOrder_whenDelivered_thenPizzaGetsDeliveredAndStatusChanges() {
    Pizza pz = new Pizza();
    pz.setStatus(Pizza.PizzaStatus.READY); 
    pz.deliver();
    assertTrue(pz.getStatus() == Pizza.PizzaStatus.DELIVERED);
}
```

### 4.5. Enum 类型的 JSON 表现形式

使用Jackson库，可以将枚举类型的JSON表示为POJO。下面的代码段显示了可以用于同一目的的Jackson批注：

```java
@JsonFormat(shape = JsonFormat.Shape.OBJECT)
public enum PizzaStatus {
    ORDERED (5){
        @Override
        public boolean isOrdered() {
            return true;
        }
    },
    READY (2){
        @Override
        public boolean isReady() {
            return true;
        }
    },
    DELIVERED (0){
        @Override
        public boolean isDelivered() {
            return true;
        }
    };
 
    private int timeToDelivery;
 
    public boolean isOrdered() {return false;}
 
    public boolean isReady() {return false;}
 
    public boolean isDelivered(){return false;}
 
    @JsonProperty("timeToDelivery")
    public int getTimeToDelivery() {
        return timeToDelivery;
    }
 
    private PizzaStatus (int timeToDelivery) {
        this.timeToDelivery = timeToDelivery;
    }
}
```

我们可以按如下方式使用 `Pizza` 和 `PizzaStatus`：

```java
Pizza pz = new Pizza();
pz.setStatus(Pizza.PizzaStatus.READY);
System.out.println(Pizza.getJsonString(pz));
```

生成 Pizza 状态以以下JSON展示：

```json
{
  "status" : {
    "timeToDelivery" : 2,           //对应的getTimeToDelivery方法
    "ready" : true,                   //对应的isReady方法
    "ordered" : false,               //isOrder方法
    "delivered" : false              //isDelivered方法
  },
  "deliverable" : true
}
```

有关枚举类型的JSON序列化/反序列化（包括自定义）的更多信息，请参阅[Jackson-将枚举序列化为JSON对象。](https://www.baeldung.com/jackson-serialize-enums)

## 5-基本数据类型与包装类

### 5.1. Java中的几种基本数据类型

Java中有8种基本数据类型，分别为：

* 6种数字类型 ：byte、short、int、long、float、double
* 1种字符类型：char
* 1种布尔型：boolean。

这八种基本类型都有对应的包装类分别为：Byte、Short、Integer、Long、Float、Double、Character、Boolean

各自占用：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210114173647533.png" alt="image-20210114173647533" style="zoom:67%;" />

对于boolean，官方文档未明确定义，它依赖于 JVM 厂商的具体实现。逻辑上理解是占用 1位，但是实际中会考虑计算机高效存储因素。


注意：

* Java 里使用 long 类型的数据一定要在数值后面加上L，否则将作为整型解析
* char a = 'h' char :单引号，String a = "hello":双引号


### 5.2. 自动装箱与拆箱

装箱：将基本类型用它们对应的引用类型包装起来；

拆箱：将包装类型转换为基本数据类型；

在前面的文章中提到，Java为每种基本数据类型都提供了对应的包装器类型。在Java SE5之前，如果要生成一个数值为10的Integer对象，必须这样进行：

```java
Integer i = new Integer(10);
```

而在从Java SE5开始就提供了自动装箱的特性，如果要生成一个数值为10的Integer对象，只需要这样就可以了：

```java
Integer i = 10;
```

这个过程中会自动根据数值创建对应的 Integer对象，这就是装箱。


那什么是拆箱呢？顾名思义，跟装箱对应，就是自动将包装器类型转换为基本数据类型：

```java
Integer i = 10;  //装箱
int n = i;   //拆箱
```

简单一点说，装箱就是  自动将基本数据类型转换为包装器类型；拆箱就是  自动将包装器类型转换为基本数据类型。

基本数据类型对应的包装器类型：
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119152638405.png" alt="image-20210119152638405" style="zoom:50%;" />

#### 1. 装箱和拆箱如何实现的

以Interger类为例，下面看一段代码：

```java
public class Main {
    public static void main(String[] args) {
        Integer i = 10;
        int n = i;
    }
}
```

反编译class文件之后得到如下内容：

```java
F:\study\java_base\out\production\java_base\test>javap -c Main
警告: 二进制文件Main包含test.Main
Compiled from "Main.java"
public class test.Main {
  public test.Main();
    Code:
       0: aload_0
       1: invokespecial #1                  // Method java/lang/Object."<init>":()V
       4: return

  public static void main(java.lang.String[]);
    Code:
       0: bipush        10
       2: invokestatic  #2                  // Method java/lang/Integer.valueOf:(I)Ljava/lang/Integer;
       5: astore_1
       6: aload_1
       7: invokevirtual #3                  // Method java/lang/Integer.intValue:()I
      10: istore_2
      11: return
}
```

>`javap` 找不到或无法加载主类 com.sun.tools.javap.Main。查看jdk的lib下是否有tools.jar包。没有该包会报错

>`javap` 的参数为class字节码文件


从反编译得到的字节码内容可以看出，在装箱的时候自动调用的是 `Integer` 的 `valueOf(int)` 方法。而在拆箱的时候自动调用的是 `Integer` 的 `intValue` 方法。其他的也类似，比如 `Double`、`Character`，不相信的朋友可以自己手动尝试一下。　　

因此可以用一句话总结装箱和拆箱的实现过程：装箱过程是通过调用包装器的 `valueOf` 方法实现的，而拆箱过程是通过调用包装器的 `xxxValue` 方法实现的。（xxx代表对应的基本数据类型）。




#### 2. 8种基本类型的包装类和对应的常量池


Java 基本类型的包装类的大部分都实现了常量池技术，即 `Byte`, `Short`, `Integer`, `Long`, `Character`, `Boolean`；如果超出对应范围仍然会去创建新的对象

- `Byte`, `Short`, `Integer`, `Long` 这4 种包装类默认创建了数值[-128，127] 的相应类型的缓存数据，
- `Character` 创建了数值在[0,127]范围的缓存数据，
- `Boolean` 直接返回`True` Or `False`。

>为啥把缓存设置为[-128，127]区间？（参见issue/461）性能和资源之间的权衡。
>1.技术规范。JLS7 5.1.7：`If the value p being boxed is an integer literal of type int between -128 and 127 inclusive (§3.10.1), or the boolean literal true or false (§3.10.3), or a character literal between '\u0000' and '\u007f' inclusive (§3.10.4), then let a and b be the results of any two boxing conversions of p . It is always the case that a == b .`
>2.性能和资源之间的权衡（当然也可以调整缓存的正向最大值，自己看 `IntegerCache` 类的实现）。

1、Boolean

```java
public static Boolean valueOf(boolean b) {
    return (b ? TRUE : FALSE);
}
```

2、Character

```java
private static class CharacterCache {         
    private CharacterCache(){}

    static final Character cache[] = new Character[127 + 1];          
    static {             
        for (int i = 0; i < cache.length; i++)                 
            cache[i] = new Character((char)i);         
    }   
}
```

3、两种浮点数类型的包装类 Float,Double 并没有实现常量池技术

Float,Double 并没有实现常量池技术,因为浮点数在区间的话有无数个

```java
Integer i1 = 33;
Integer i2 = 33;
System.out.println(i1 == i2);// 输出 true
Integer i11 = 333;
Integer i22 = 333;
System.out.println(i11 == i22);// 输出 false
Double i3 = 1.2;
Double i4 = 1.2;
System.out.println(i3 == i4);// 输出 false
```

4、Integer 缓存源代码

Integer i1 = 40；Java 在编译的时候会直接将代码封装成 `Integer i1=Integer.valueOf(40);`，从而使用常量池中的对象。

```java
/**
*此方法将始终缓存-128 到 127（包括端点）范围内的值，并可以缓存此范围之外的其他值。
*/
public static Integer valueOf(int i) {
	if (i >= IntegerCache.low && i <= IntegerCache.high)
		return IntegerCache.cache[i + (-IntegerCache.low)];
	return new Integer(i);
}
```

5、应用场景

```java
Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);//输出 false
```

- Integer i1=40；Java 在编译的时候会直接将代码封装成 `Integer i1=Integer.valueOf(40);`，从而使用常量池中的对象。
- Integer i1 = new Integer(40);这种情况下会创建新的对象。

Integer 比较更丰富的一个例子:

```java
  Integer i1 = 40;
  Integer i2 = 40;
  Integer i3 = 0;
  Integer i4 = new Integer(40);
  Integer i5 = new Integer(40);
  Integer i6 = new Integer(0);

  System.out.println("i1=i2   " + (i1 == i2));
  System.out.println("i1=i2+i3   " + (i1 == i2 + i3));
  System.out.println("i1=i4   " + (i1 == i4));
  System.out.println("i4=i5   " + (i4 == i5));
  System.out.println("i4=i5+i6   " + (i4 == i5 + i6));   
  System.out.println("40=i5+i6   " + (40 == i5 + i6));     
```

结果：

```java
i1=i2   true
i1=i2+i3   true
i1=i4   false
i4=i5   false
i4=i5+i6   true
40=i5+i6   true
```

解释：语句 i4 == i5 + i6，因为+这个操作符不适用于 Integer 对象，首先 i5 和 i6 进行自动拆箱操作，进行数值相加，即 i4 == 40。然后 Integer 对象无法与数值进行直接比较，所以 i4 自动拆箱转为 int 值 40，最终这条语句转为 40 == 40 进行数值比较。

#### 3. 包装类值的比较

所有包装类对象值的比较必须使用equals方法。先看下面这个例子：

```java
Integer x = 3;
Integer y = 3;
System.out.println(x == y);// true
Integer a = new Integer(3);
Integer b = new Integer(3);
System.out.println(a == b);//false
System.out.println(a.equals(b));//true
```

当使用自动装箱方式创建一个Integer对象时，当数值在-128 ~127时，会将创建的 Integer 对象缓存起来，当下次再出现该数值时，直接从缓存中取出对应的Integer对象。所以上述代码中，x和y引用的是相同的Integer对象。

Integer a = new Integer(3);Integer b = new Integer(3); 重新创建了Integer对象，a和b引用的是相同的Integer对象

Integer重写了equals方法

```java
public boolean equals(Object obj) {
	if (obj instanceof Integer) {
		return value == ((Integer)obj).intValue();
	}
	return false;
}
```

>注意：如果你的IDE(IDEA/Eclipse)上安装了阿里巴巴的p3c插件，这个插件如果检测到你用 == 的话会报错提示，推荐安装一个这个插件，很不错。

#### 4. 面试中相关的问题

虽然大多数人对装箱和拆箱的概念都清楚，但是在面试和笔试中遇到了与装箱和拆箱的问题却不一定会答得上来。下面列举一些常见的与装箱/拆箱有关的面试题。

1、这段代码的输出结果是什么？

```java
public class Main {
    public static void main(String[] args) {
         
        Integer i1 = 100;
        Integer i2 = 100;
        Integer i3 = 200;
        Integer i4 = 200;
         
        System.out.println(i1==i2);   //true
        System.out.println(i3==i4);  //false
    }
}
```

输出结果表明i1和i2指向的是同一个对象，而i3和i4指向的是不同的对象。此时只需一看源码便知究竟，下面这段代码是Integer的valueOf方法的具体实现：

```java
public static Integer valueOf(int i) {
	if (i >= IntegerCache.low && i <= IntegerCache.high)
		return IntegerCache.cache[i + (-IntegerCache.low)];
	return new Integer(i);
}
```

IntegerCache类的实现为

```java
private static class IntegerCache {
	static final int low = -128;
	static final int high;
	static final Integer cache[];

	static {
		// high value may be configured by property
		int h = 127;
		String integerCacheHighPropValue =
			sun.misc.VM.getSavedProperty("java.lang.Integer.IntegerCache.high");
		if (integerCacheHighPropValue != null) {
			try {
				int i = parseInt(integerCacheHighPropValue);
				i = Math.max(i, 127);
				// Maximum array size is Integer.MAX_VALUE
				h = Math.min(i, Integer.MAX_VALUE - (-low) -1);
			} catch( NumberFormatException nfe) {
				// If the property cannot be parsed into an int, ignore it.
			}
		}
		high = h;

		cache = new Integer[(high - low) + 1];
		int j = low;
		for(int k = 0; k < cache.length; k++)
			cache[k] = new Integer(j++);

		// range [-128, 127] must be interned (JLS7 5.1.7)
		assert IntegerCache.high >= 127;
	}

	private IntegerCache() {}
}
```

>从这2段代码可以看出，在通过valueOf方法创建Integer对象的时候，如果数值在[-128,127]之间，便返回指向IntegerCache.cache中已经存在的对象的引用；否则创建一个新的Integer对象。

上面的代码中i1和i2的数值为100，因此会直接从cache中取已经存在的对象，所以i1和i2指向的是同一个对象，而i3和i4则是分别指向不同的对象。

2、这段代码的输出结果是什么？

```java
public class Main {
    public static void main(String[] args) {
         
        Double i1 = 100.0;
        Double i2 = 100.0;
        Double i3 = 200.0;
        Double i4 = 200.0;
         
        System.out.println(i1==i2);   //false
        System.out.println(i3==i4);   //false
    }
}
```

至于具体为什么，读者可以去查看Double类的valueOf的实现。在这里只解释一下为什么Double类的valueOf方法会采用与Integer类的valueOf方法不同的实现。很简单：在某个范围内的整型数值的个数是有限的，而浮点数却不是。


>注意，Integer、Short、Byte、Character、Long这几个类的valueOf方法的实现是类似的。Double、Float的valueOf方法的实现是类似的。

3、这段代码输出结果是什么：

```java
public class Main {
    public static void main(String[] args) {
         
        Boolean i1 = false;
        Boolean i2 = false;
        Boolean i3 = true;
        Boolean i4 = true;
         
        System.out.println(i1==i2);  //true
        System.out.println(i3==i4);  //true
    }
}
```

同样地，看了Boolean类的源码也会一目了然。下面是Boolean的valueOf方法的具体实现：

```java
public static Boolean valueOf(boolean b) {
        return (b ? TRUE : FALSE);
}
```

而其中的 TRUE 和FALSE又是什么呢？在Boolean中定义了2个静态成员属性：

```java
public static final Boolean TRUE = new Boolean(true);

/** 
 * The <code>Boolean</code> object corresponding to the primitive 
 * value <code>false</code>. 
 */
 public static final Boolean FALSE = new Boolean(false);
```

4、谈谈Integer i = new Integer(xxx)和Integer i =xxx;这两种方式的区别

- 第一种方式不会触发自动装箱的过程；而第二种方式会触发；
- 在执行效率和资源占用上的区别。第二种方式的执行效率和资源占用在一般性情况下要优于第一种情况（注意这并不是绝对的）。

5、下面程序的输出结果是什么？

```java
public class Main {
    public static void main(String[] args) {
         
        Integer a = 1;
        Integer b = 2;
        Integer c = 3;
        Integer d = 3;
        Integer e = 321;
        Integer f = 321;
        Long g = 3L;
        Long h = 2L;
         
        System.out.println(c==d);   //true
        System.out.println(e==f);    //false
        System.out.println(c==(a+b));  //true
        System.out.println(c.equals(a+b));  //true
        System.out.println(g==(a+b));  //true
        System.out.println(g.equals(a+b));  //false
        System.out.println(g.equals(a+h));  //true
    }
}
```

>当 "=="运算符的两个操作数都是 包装器类型的引用，则是比较指向的是否是同一个对象，而如果其中有一个操作数是表达式（即包含算术运算）则比较的是数值（即会触发自动拆箱的过程）
>另外，equals会对基本类型进行包装，对于包装器类型，equals方法并不会进行类型转换


第一个和第二个输出结果没有什么疑问。第三句由于  a+b包含了算术运算，因此会触发自动拆箱过程（会调用intValue方法），因此它们比较的是数值是否相等。而对于c.equals(a+b)会先触发自动拆箱过程，再触发自动装箱过程，也就是说a+b，会先各自调用intValue方法，得到了加法运算后的数值之后，便调用Integer.valueOf方法，再进行equals比较。同理对于后面的也是这样，不过要注意倒数第二个和最后一个输出的结果（如果数值是int类型的，装箱过程调用的是Integer.valueOf；如果是long类型的，装箱调用的Long.valueOf方法）。

### 5.3. 基本数据类型与包装数据类型的使用标准

Reference:《阿里巴巴Java开发手册》

- 【强制】所有的 POJO 类属性必须使用包装数据类型。
- 【强制】RPC 方法的返回值和参数必须使用包装数据类型。
- 【推荐】所有的局部变量使用基本数据类型。

比如我们如果自定义了一个Student类,其中有一个属性是成绩score,如果用Integer而不用int定义,一次考试,学生可能没考,值是null,也可能考了,但考了0分,值是0,这两个表达的状态明显不一样.

说明 : POJO 类属性没有初值是提醒使用者在需要使用时，必须自己显式地进行赋值，任何 `NPE(Null Pointer Exception)` 问题，或者入库检查，都由使用者来保证。

正例 : 数据库的查询结果可能是 null，因为自动装箱，这会导致null值出现，根据不同场景进行处理，但是不建议在pojo里面处理，要保证pojo的完整干净。

反例 : 比如显示成交总额涨跌情况，即正负 x%，x 为基本数据类型，调用的 RPC 服务，调用不成功时，返回的是默认值，页面显示为 0%，这是不合理的，应该显示成中划线。所以包装数据类型的 null 值，能够表示额外的信息，如:远程调用失败，异常退出。

### 5.4. BigDecimal用法

1、BigDecimal 的用处

《阿里巴巴Java开发手册》中提到：浮点数之间的等值判断，基本数据类型不能用==来比较，包装数据类型不能用 equals 来判断。 具体原理和浮点数的编码方式有关，这里就不多提了，我们下面直接上实例：

```java
float a = 1.0f - 0.9f;
float b = 0.9f - 0.8f;
System.out.println(a);// 0.100000024
System.out.println(b);// 0.099999964
System.out.println(a == b);// false
```
具有基本数学知识的我们很清楚的知道输出并不是我们想要的结果（精度丢失），我们如何解决这个问题呢？一种很常用的方法是：使用使用 BigDecimal 来定义浮点数的值，再进行浮点数的运算操作。

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
BigDecimal c = new BigDecimal("0.8");
BigDecimal x = a.subtract(b);// 0.1
BigDecimal y = b.subtract(c);// 0.1
System.out.println(x.equals(y));// true 
```

2、`BigDecimal` 的大小比较

`a.compareTo(b)` : 返回 -1 表示小于，0 表示 等于， 1表示 大于。

```java
BigDecimal a = new BigDecimal("1.0");
BigDecimal b = new BigDecimal("0.9");
System.out.println(a.compareTo(b));// 1
```

3、BigDecimal 保留几位小数

通过 `setScale`方法设置保留几位小数以及保留规则。保留规则有挺多种，不需要记，IDEA会提示。

```java
BigDecimal m = new BigDecimal("1.255433");
BigDecimal n = m.setScale(3,BigDecimal.ROUND_HALF_DOWN);
System.out.println(n);// 1.255
```

4、BigDecimal 的使用注意事项

注意：我们在使用BigDecimal时，为了防止精度丢失，推荐使用它的 **BigDecimal(String)** 构造方法来创建对象。《阿里巴巴Java开发手册》对这部分内容也有提到如下图所示。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119154633977.png" alt="image-20210119154633977" style="zoom:50%;" />

5、总结

BigDecimal 主要用来操作（大）浮点数，BigInteger 主要用来操作大整数（超过 long 类型）。

BigDecimal 的实现利用到了 BigInteger, 所不同的是 BigDecimal 加入了小数位的概念

## 6-Java反射机制

1、反射机制介绍

JAVA 反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种动态获取类的信息以及动态调用对象的方法的功能称为 java 语言的反射机制。

>反射就是把java类中的各种成分映射成一个个的Java对象

前提条件： 必须先得到代表的字节码的Class，Class类用于表示.class文件（字节码）

2、获取 `Class` 对象的两种方式

如果我们动态获取到这些信息，我们需要依靠 Class 对象。Class 类对象将一个类的方法、变量等信息告诉运行的程序。Java 提供了两种方式获取 Class 对象:

- 知道具体类的情况下可以使用：


```java
Class alunbarClass = TargetObject.class;
```

但是我们一般是不知道具体类的，基本都是通过遍历包下面的类来获取 Class 对象

- 通过 `Class.forName()` 传入类的路径获取：


```java
Class alunbarClass1 = Class.forName("cn.javaguide.TargetObject");
```

3、代码实例

简单用代码演示一下反射的一些操作!

1.创建一个我们要使用反射操作的类 `TargetObject`：

```java
package cn.javaguide;

public class TargetObject {
    private String value;

    public TargetObject() {
        value = "JavaGuide";
    }

    public void publicMethod(String s) {
        System.out.println("I love " + s);
    }

    private void privateMethod() {
        System.out.println("value is " + value);
    }
}
```

2.使用反射操作这个类的方法以及属性

```java
package cn.javaguide;

import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class Main {
    public static void main(String[] args) throws Exception {
        /**
         * 获取TargetObject类的Class对象并且创建TargetObject类实例
         */
        Class<?> tagetClass = Class.forName("domain.TargetObject");
        TargetObject targetObject = (TargetObject) tagetClass.newInstance();
        /**
         * 获取所有类中所有定义的方法(包括私有方法)
         */
        Method[] methods = tagetClass.getDeclaredMethods();
        for (Method method : methods) {
            System.out.println(method.getName());
        }
        /**
         * 获取 指定方法名和参数类型 的public方法并调用方法
         */
        Method publicMethod = tagetClass.getDeclaredMethod("publicMethod",String.class);
        publicMethod.invoke(targetObject, "JavaGuide");
        
        /**
         * 获取指定属性名的属性并对属性进行修改
         */
        Field field = tagetClass.getDeclaredField("value");
        
        //为了对类中的参数进行修改我们取消安全检查
        field.setAccessible(true);
        field.set(targetObject, "JavaGuide");
        
        /**
         * 获取指定方法名的private方法并调用方法
         */
        Method privateMethod = tagetClass.getDeclaredMethod("privateMethod");
        
        //为了调用private方法我们取消安全检查
        privateMethod.setAccessible(true);
        privateMethod.invoke(targetObject);
    }
}

```

输出内容：

```
publicMethod
privateMethod
I love JavaGuide
value is JavaGuide
```

4、静态编译和动态编译

- 静态编译： 在编译时确定类型，绑定对象
- 动态编译： 在运行时确定类型，绑定对象

两者的区别在于，动态编译可以最大程度地支持多态，而多态最大的意义在于降低类的耦合性，因此反射的优点就很明显了：解耦以及提高代码的灵活性

5、反射机制优缺点

- 优点： 运行期类型的判断，动态加载类，提高代码灵活度。
- 缺点： 1. 性能瓶颈：反射相当于一系列解释操作，通知 JVM 要做的事情，性能比直接的 java 代码要慢很多。2. 安全问题，让我们可以动态操作改变类的属性同时也增加了类的安全隐患。

6、反射的应用场景

**反射是框架设计的灵魂。**

在我们平时的项目开发过程中，基本上很少会直接使用到反射机制，但这不能说明反射机制没有用，实际上有很多设计、开发都与反射机制有关，例如模块化的开发，通过反射去调用对应的字节码；动态代理设计模式也采用了反射机制，还有我们日常使用的 Spring／Hibernate 等框架也大量使用到了反射机制。

举例：

1. 我们在使用 JDBC 连接数据库时使用 `Class.forName()` 通过反射加载数据库的驱动程序；
2. Spring 框架的 IOC（动态加载管理 Bean）创建对象以及 AOP（动态代理）功能都和反射有联系；
3. 动态配置实例的属性；
    1. setter依赖注入： 利用Java的反射机制调用对象的某个set方法，并将值设置进去
4. ......

7、推荐阅读：

- [Java反射使用总结]( https://zhuanlan.zhihu.com/p/80519709)
- [Reflection：Java 反射机制的应用场景](https://segmentfault.com/a/1190000010162647?utm_source=tuicool&utm_medium=referral)
- [Java 基础之—反射（非常重要）](https://blog.csdn.net/sinat_38259539/article/details/71799078)

## 7-Java IO流

### 7.1. Linux IO

#### 1. 相关概念

1、操作系统的内核

操作系统的内核是操作系统的核心部分。它负责系统的内存，硬件设备，文件系统以及应用程序的管理。

2、操作系统的用户态与内核态

unix 与 linux 的体系架构：用户态与内核态。

用户态与内核态是操作系统对执行权限进行分级后的不同的运行模式。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119155818294.png" alt="image-20210119155818294" style="zoom:50%;" />

3、为什么要有用户态与内核态?

在 cpu 的所有指令中，有些指令是非常危险的，如果使用不当，将会造成系统崩溃等后果。为了避免这种情况发生，cpu 将指令划分为特权级(内核态)指令和非特权级(用户态)指令。

对于那些危险的指令只允许内核及其相关模块调用，对于那些不会造成危险的指令，就允许用户应用程序调用。

- 内核态(核心态,特权态): 内核态是操作系统内核运行的模式。 内核态控制计算机的硬件资源，如硬件设备，文件系统等等，并为上层应用程序提供执行环境。
- 用户态: 用户态是用户应用程序运行的状态。 应用程序必须依托于内核态运行,因此用户态的态的操作权限比内核态是要低的，如磁盘，文件等，访问操作都是受限的。
- 系统调用: 系统调用是操作系统为应用程序提供能够访问到内核态的资源的接口。

4、用户态切换到内核态的几种方式

- 系统调用: 系统调用是用户态主动要求切换到内核态的一种方式，用户应用程序通过操作系统调用内核为上层应用程序开放的接口来执行程序。
- 异常: 当 cpu 在执行用户态的应用程序时，发生了某些不可知的异常。于是当前用户态的应用进程切换到处理此异常的内核的程序中去。
- 硬件设备的中断: 当硬件设备完成用户请求后，会向 cpu 发出相应的中断信号，这时 cpu 会暂停执行下一条即将要执行的指令，转而去执行与中断信号对应的应用程序，如果先前执行的指令是用户态下程序的指令，那么这个转换过程也是用户态到内核台的转换。

5、阻塞和非阻塞

1. 阻塞: 一个线程调用一个方法计算 1 - 100 的和，如果该方法没有返回结果， 那么调用方法的线程就一直等待直到该方法执行完毕。
2. 非阻塞: 一个线程调用一个方法计算 1 - 100 的和，该方法立刻返回，如果方法返回没有结果，调用者线程也无需一直等待该方法的结果，可以执行其他任务，但是在方法返回结果之前， 线程仍然需要轮询的检查方法是否已经有结果。

结论: 阻塞与非阻塞针对调用者的立场而言。

6、同步与异步

1. 同步: 一个线程调用一个方法计算 1 - 100 的和，如果方法没有计算完，就不返回。
2. 异步: 一个线程调用一个方法计算 1 - 100 的和，该方法立刻返回，但是由于方法没有返回结果， 所以就需要被调用的这个方法来通知调用线程 1 - 100 的结果， 或者线程在调用方法的时候指定一个回调函数来告诉被调用的方法执行完后就执行回调函数。

结论:同步和异步是针对被调用者的立场而言的。

#### 2. Linux IO 模型

我们常说的IO，指的是文件的输入和输出，但是在操作系统层面是如何定义IO的呢？到底什么样的过程可以叫做是一次IO呢？

拿一次磁盘文件读取为例，我们要读取的文件是存储在磁盘上的，我们的目的是把它读取到内存中。可以把这个步骤简化成把数据从硬件（硬盘）中读取到用户空间中。

Linux 下共有 5 种 IO 模型:

1. 阻塞 IO
2. 非阻塞 IO
3. IO 多路复用
4. 信号驱动 IO
5. 异步 IO

##### 1. 阻塞 IO

映射到Linux操作系统中，这就是一种最简单的IO模型，即阻塞IO。 阻塞 I/O 是最简单的 I/O 模型，一般表现为进程或线程等待某个条件，如果条件不满足，则一直等下去。条件满足，则进行下一步操作。

阻塞 IO 是很常见的一种 IO 模型。在这种模型中，<u>用户态的应用程序会执行一个操作系统的调用，检查内核的数据是否准备好。如果内核的数据已经准备好，就把数据复制到用户应用进程。如果内核没有准备好数据，那么用户应用进程(线程)就阻塞，直到内核准备好数据并把数据从内核复制到用户应用进程</u>，最后应用程序再处理数据。

>网络中的数据是否传输完成由TCP协议三次握手去确定。数据通过网卡接收。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119160901776.png" alt="image-20210119160901776" style="zoom:50%;" />

>应用进程通过系统调用 `recvfrom` 接收数据，但由于内核还未准备好数据报，应用进程就会阻塞住，直到内核准备好数据包，`recvfrom` 完成数据报复制工作，应用进程才能结束阻塞状态。

**阻塞 IO 是同步阻塞的。**

1. 阻塞 IO 的同步体现在: **内核只有准备好数据并把数据复制到用户应用进程才会返回。**

2. 阻塞 IO 的阻塞体现在:**用户应用进程等待内核准备数据和把数据从用户态拷贝到内核态的这整个过程，用户应用进程都必须一直等待。** 当然,如果是本地磁盘 IO,内核准备数据的时间可能会很短。但网络 IO 就不一样了，因为服务端不知道客户端何时发送数据，内核就仍需要等待 socket 数据，时间就可能会很长。

**阻塞 IO 的优点是对于数据是能够保证无延时的，因为应用程序进程会一直阻塞直到 IO 完成。** 但应用程序的阻塞就意味着应用程序进程无法执行其他任务，这会大大降低程序性能。一个不太可行的办法是为每个客户端 socket 都分配一个线程，这样就会提升 server 处理请求的能力。不过操作系统的线程资源是有限的，如果请求过多，可能造成线程资源耗尽，系统卡死等后果。

##### 2. 非阻塞 IO(网络 IO 模型)


应用进程与内核交互，目的未达到之前，不再一味的等着，而是直接返回。然后通过轮询的方式，不停的去问内核数据准备有没有准备好。如果某一次轮询发现数据已经准备好了，那就把数据拷贝到用户空间中。

在非阻塞 IO 模型中，用户态的应用程序也会执行一个操作系统的调用，检查内核的数据是否准备完成。<u>如果内核没有准备好数据,内核会立刻返回结果,用户应用进程不用一直阻塞等待内核准备数据，而是可以执行其他任务,但仍需要不断的向内核发起系统调用，检测数据是否准备好，这个过程就叫轮询</u>。轮询直到内核准备好数据，然后内核把数据拷贝到用户应用进程，再进行数据处理。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119160925157.png" alt="image-20210119160925157" style="zoom:50%;" />

>应用进程通过 `recvfrom` 调用不停的去和内核交互，直到内核准备好数据。如果没有准备好，内核会返回 `EWOULDBLOCK`，应用进程在得到 `EWOULDBLOCK` 后，过一段时间再发送 `recvfrom` 请求。在两次发送请求的时间段，进程可以先做别的事情。


非阻塞 IO 的非阻塞体现在: **用户应用进程不用阻塞在对内核的系统调用上**

非阻塞 IO 的优点在于用户应用进程在轮询阶段可以执行其它任务。但这也是它的缺点，轮询就代表着用户应用进程不是时刻都会发起系统调用。**可能数据准备好了，而用户应用进程可能等待其它任务执行完毕才会发起系统调用，这就意味着数据可能会被延时获取。**


##### 3. IO 多路复用(网络 IO 模型)

在 IO 多路复用模型中, 用户应用进程会调用操作系统的 `select/poll/epoll`  函数,它会使内核同步轮询指定 socket 连接(socket IO)，直至监听的 socket 的任意一个连接有数据可读或可写，`select/poll/epoll`  函数才会返回,用户应用进程也会阻塞的等待 `select/poll/epoll` 函数返回。

当 `select/poll/epoll` 函数返回后，即某个socket连接所需的数据准备好之后，用户应用进程就会发起系统调用，将数据直接复制到用户进程内，然后进行数据处理。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119160944487.png" alt="image-20210119160944487" style="zoom:50%;" />

> 多个进程的socket IO可以注册到同一个管道上，这个管道会统一和内核进行交互。当管道中的某一个请求需要的数据准备好之后，进程再把对应的数据拷贝到用户空间中。

> IO多路转接是多了一个 `select` 函数，多个进程的IO可以注册到同一个 `select` 上，当用户进程调用该 `select`，`select` 会监听所有注册好的IO，如果所有被监听的IO需要的数据都没有准备好时，`select` 调用进程会阻塞。当任意一个IO所需的数据准备好之后，select调用就会返回，然后进程在通过 `recvfrom` 来进行数据拷贝。进程在发出 `select` 后，要等到 `select` 监听的所有IO操作中至少有一个需要的数据准备好，才会有返回，并且也需要再次发送 `recvfrom` 请求去进行文件的拷贝。


**IO 多路复用模型是同步阻塞的**

1. IO 多路复用模型的同步体现在: **select 函数只有监听到某个 socket 有事件才会返回。**

2. IO 多路复用模型的阻塞体现在: **用户应用进程会阻塞在对 select 函数上的调用上。**

**IO 多路复用的优点在于内核可以处理多个 socket IO，相当于一个用户进程(线程)就可以处理多个 socket 连接。**

这样不仅降低了系统的开销，并且对于需要高并发的应用是非常有利的。而非阻塞 IO 和阻塞 IO 的一个用户应用进程只能处理一个 socket 连接，要想处理多个 socket 连接，只能新开进程或线程，但这样很消耗系统资源。

>在 IO 多路复用模型中，如果某个socket连接所需的数据准备好之后，用户应用进程发起 `recvfrom`  系统调用，要以**非阻塞IO**的形式去读取内核中已经准备好的数据。

**PS: 在 IO 多路复用模型中, socket 一般应该为非阻塞的，这就是 Java 中 NIO 被称为非阻塞 IO 的原因。但实际上 NIO 属于 IO 多路复用，它是同步阻塞的 IO。具体原因见 [知乎讨论](https://www.zhihu.com/question/37271342)**

**PS: select/poll/epoll 函数是 IO 多路复用模型的基础，所以如果想深入了解 IO 多路复用模型，就需要了解这 3 个函数以及它们的优缺点。**




##### 4. 信号驱动 IO(网络 IO 模型)

在信号驱动 IO 模型中，<u>用户应用进程发起 sigaction 系统调用,内核收到并立即返回。用户应用进程可以继续执行其他任务，不会阻塞。当内核准备好数据后向用户应用进程发送 SIGIO 信号，应用进程收到信号后，发起系统调用，将数据从内核拷贝到用户进程，然后进行数据处理</u>。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161000414.png" alt="image-20210119161000414" style="zoom:50%;" />


>应用进程预先向内核注册一个信号处理函数，然后返回用户进程，并且不阻塞，当内核数据准备就绪时会发送一个信号给进程，用户进程便在信号处理函数中开始把数据拷贝的用户空间中。

>个人感觉在内核收到系统调用就立刻返回这一点很像异步 IO 的方式了，不过与异步 IO 仍有很大差别。


信号驱动难道不是异步的么？ 信号驱动，内核是在数据准备好之后通知进程，然后进程再通过recvfrom操作进行数据拷贝。我们可以认为数据准备阶段是异步的，但是，数据拷贝操作是同步的。所以，整个IO过程也不能认为是异步的。


##### 5. 异步 IO

阻塞IO模型、非阻塞IO模型、IO复用模型和信号驱动IO模型都是同步的IO模型。原因是因为，无论以上那种模型，真正的数据拷贝过程，都是同步进行的


应用进程把IO请求传给内核后，完全由内核去操作文件拷贝。内核完成相关操作后，会发信号告诉应用进程本次IO已经完成。


在异步 IO 模型中，<u>用户进程发起 `aio_read` 系统调用，无论内核的数据是否准备好，都会立即返回。用户应用进程不会阻塞,可以继续执行其他任务。当内核准备好数据,**内核会直接把数据复制到用户应用进程**。最后内核会通知用户应用进程 IO 完成。</u>

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161022554.png" alt="image-20210119161022554" style="zoom:50%;" />


>用户进程发起`aio_read`操作之后，给内核传递描述符、缓冲区指针、缓冲区大小等，告诉内核当整个操作完成时，如何通知进程，然后就立刻去做其他事情了。当内核收到 `aio_read` 后，会立刻返回，然后内核开始等待数据准备，数据准备好以后，直接把数据拷贝到用户应用进程，然后再通知进程本次IO已经完成。


**异步 IO 的异步体现在:内核不用等待数据准备好就立刻返回，所以内核肯定需要在 IO 完成后通知用户应用进程。**


##### 6. 5种IO模型对比

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161041504.png" alt="image-20210119161041504" style="zoom:50%;" />


##### 7.  Java NIO模型

Java NIO模式: IO多路复用 + 非阻塞IO + 应用层buffer

IO 多路复用 ： 比如 调用了一个 `select` 函数，假如当有套接口可读时， select 函数就返回了，告诉我们套接口已经可读，然后我们去读这个套接口，可以用阻塞的read或者非阻塞的 read。

1、Java NIO模型为什么使用非阻塞IO进行read?

* 非阻塞 I/O 的处理方式：循环的 read 或 accept，如果内核没有准备好数据则立即返回，直到读完所有的数据（抛出 EWOULDBLOCK 异常）。
* 阻塞 I/O 的处理方式：每次只能调用一次 read 或 accept，如果内核没有准备好数据则阻塞，有数据则读完所有数据到应用层。

select 返回可读，和 read 去读，这是两个独立的系统调用，两个操作之间是有窗口的，也就是说 select 返回可读，紧接着去 read，不能保证一定可读。如果不用非阻塞，程序会永远卡在read上。

* 惊群现象，就是一个典型场景，多个进程或者线程通过 select 或者 epoll 监听一个 listen socket，当有一个新连接完成三次握手之后，所有监听该端口的进程或线程都会通过 select 或者 epoll 被唤醒，但是最终只有一个进程或者线程 accept 到这个新连接，若是采用了阻塞 I/O，没有 accept 到连接的进程或者线程就 block 住了,无法返回 select。


*  多路复用只会告诉你 fd 对应的 socket 可读了，但不会告诉你有多少的数据可读。
    *  假如socket的读缓冲区已经有足够多的数据，需要read多次才能读完，如果是非阻塞可以在循环里读取，不用担心阻塞在read上，等到errno被置为EWOULDBLOCK的时候break，安全返回select。但如果是阻塞IO，只敢读取一次，因为如果读取没有数据的fd，read会阻塞，无法返回 select，这样就只能期待着多次从select返回，每次只读一次，效率低下。而且，如果是ET模式，还会造成数据无人处理，导致饥饿。

### 7.2. BIO,NIO,AIO

Java 中的 BIO、NIO和 AIO 理解为是 Java 语言对操作系统的各种 IO 模型的封装。程序员在使用这些 API 的时候，不需要关心操作系统层面的知识，也不需要根据不同操作系统编写不同的代码。只需要使用Java的API就可以了。

在讲 BIO,NIO,AIO 之前先来回顾一下这样几个概念：同步与异步，阻塞与非阻塞。

1、同步与异步

关于同步和异步的概念解读困扰着很多程序员，大部分的解读都会带有自己的一点偏见。参考了 [Stackoverflow](https://stackoverflow.com/questions/748175/asynchronous-vs-synchronous-execution-what-does-it-really-mean)相关问题后对原有答案进行了进一步完善：

> When you execute something synchronously, you wait for it to finish before moving on to another task. When you execute something asynchronously, you can move on to another task before it finishes.
>
> 当你同步执行某项任务时，你需要等待其完成才能继续执行其他任务。当你异步执行某些操作时，你可以在完成另一个任务之前继续进行。

- 同步 ：两个同步任务相互依赖，并且一个任务必须以依赖于另一任务的某种方式执行。 比如在`A->B`事件模型中，你需要先完成 A 才能执行B。 再换句话说，同步调用中被调用者未处理完请求之前，调用不返回，调用者会一直等待结果的返回。
- 异步： 两个异步的任务完全独立的，一方的执行不需要等待另外一方的执行。再换句话说，异步调用中一调用就返回结果不需要等待结果返回，当结果返回的时候通过回调函数或者其他方式拿着结果再做相关事情，

2、阻塞和非阻塞

- 阻塞： 阻塞就是发起一个请求，调用者一直等待请求结果返回，也就是当前线程会被挂起，无法从事其他任务，只有当条件就绪才能继续。
- 非阻塞： 非阻塞就是发起一个请求，调用者不用一直等着结果返回，可以先去干其他事情。


如何区分 “同步/异步 ”和 “阻塞/非阻塞” 呢？

同步/异步是从行为角度描述事物的，而阻塞和非阻塞描述的当前事物的状态（等待调用结果时的状态）。

#### 1. BIO (Blocking I/O)

同步阻塞I/O模式，数据的读取写入必须阻塞在一个线程内等待其完成。

##### 1.1 传统 BIO


采用 **BIO 通信模型** 的服务端，通常由一个独立的 Acceptor 线程启动并负责监听客户端的连接。我们一般通过在`while(true)` 循环中服务端会调用 `accept()` 方法等待接收客户端的连接的方式监听请求，<u>请求一旦接收到一个连接请求，就可以建立通信套接字在这个通信套接字上进行读写操作，此时不能再接收其他客户端连接请求，只能等待同当前连接的客户端的操作执行完成（主要原因是`socket.accept()`、`socket.read()`、`socket.write()` 涉及的三个主要函数都是同步阻塞的）</u> 。

 **BIO通信（一请求一应答）模型：** 可以通过多线程来支持多个客户端的连接，如下图所示。
<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161422021.png" alt="image-20210119161422021" style="zoom:60%;" />

如果要让 **BIO 通信模型** 能够同时处理多个客户端请求，就必须使用多线程（主要原因是`socket.accept()`、`socket.read()`、`socket.write()` 涉及的三个主要函数都是同步阻塞的），也就是说它在接收到客户端连接请求之后为每个客户端创建一个新的线程进行链路处理，处理完成之后，通过输出流返回应答给客户端，线程销毁。这就是典型的 **一请求一应答通信模型** 。我们可以设想一下如果这个连接不做任何事情的话就会造成不必要的线程开销，不过可以通过 **线程池机制** 改善，线程池还可以让线程的创建和回收成本相对较低。使用`FixedThreadPool` 可以有效的控制了线程的最大数量，保证了系统有限的资源的控制，实现了N(客户端请求数量):M(处理客户端请求的线程数量)的伪异步I/O模型（N 可以远远大于 M），下面一节"伪异步 BIO"中会详细介绍到。

**我们再设想一下当客户端并发访问量增加后这种模型会出现什么问题？**

在 Java 虚拟机中，线程是宝贵的资源，线程的创建和销毁成本很高，除此之外，线程的切换成本也是很高的。尤其在 Linux 这样的操作系统中，线程本质上就是一个进程，创建和销毁线程都是重量级的系统函数。如果并发访问量增加会导致线程数急剧膨胀可能会导致线程堆栈溢出、创建新线程失败等问题，最终导致进程宕机或者僵死，不能对外提供服务。

##### 1.2 伪异步 IO

为了解决同步阻塞I/O面临的一个链路需要一个线程处理的问题，后来有人对它的线程模型进行了优化一一一后端通过一个线程池来处理多个客户端的请求接入，形成客户端个数M：线程池最大线程数N的比例关系，其中M可以远远大于N.通过线程池可以灵活地调配线程资源，设置线程的最大值，防止由于海量并发接入导致线程耗尽。

伪异步IO模型图(图源网络，原出处不明)：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161438927.png" alt="image-20210119161438927" style="zoom: 50%;" />![image-20210119161520871](C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161520871.png)

采用线程池和任务队列可以实现一种叫做伪异步的 I/O 通信框架，它的模型图如上图所示。当有新的客户端接入时，将客户端的 Socket 封装成一个Task（该任务实现java.lang.Runnable接口）投递到后端的线程池中进行处理，JDK 的线程池维护一个消息队列和 N 个活跃线程，对消息队列中的任务进行处理。由于线程池可以设置消息队列的大小和最大线程数，因此，它的资源占用是可控的，无论多少个客户端并发访问，都不会导致资源的耗尽和宕机。

伪异步I/O通信框架采用了线程池实现，因此避免了为每个请求都创建一个独立线程造成的线程资源耗尽问题。不过因为它的底层仍然是同步阻塞的BIO模型，因此无法从根本上解决问题。

##### 1.3 代码示例

下面代码中演示了BIO通信（一请求一应答）模型。我们会在客户端创建多个线程依次连接服务端并向其发送"当前时间+:hello world"，服务端会为每个客户端线程创建一个线程来处理。代码示例出自闪电侠的博客，原地址如下：        

[https://www.jianshu.com/p/a4e03835921a](https://www.jianshu.com/p/a4e03835921a)

**客户端**

```java
public class IOClient {

  public static void main(String[] args) {
    // TODO 创建多个线程，模拟多个客户端连接服务端
    new Thread(() -> {
      try {
        Socket socket = new Socket("127.0.0.1", 3333);
        while (true) {
          try {
            socket.getOutputStream().write((new Date() + ": hello world").getBytes());
            Thread.sleep(2000);
          } catch (Exception e) {
          }
        }
      } catch (IOException e) {
      }
    }).start();

  }
}
```

**服务端**

```java
/**
 * @author 闪电侠
 * @date 2018年10月14日
 * @Description: 服务端
 */
public class IOServer {

  public static void main(String[] args) throws IOException {
    // TODO 服务端处理客户端连接请求
    ServerSocket serverSocket = new ServerSocket(3333);

    // 接收到客户端连接请求之后为每个客户端创建一个新的线程进行链路处理
    new Thread(() -> {
      while (true) {
        try {
          // 阻塞方法获取新的连接
          Socket socket = serverSocket.accept();

          // 每一个新的连接都创建一个线程，负责读取数据
          new Thread(() -> {
            try {
              int len;
              byte[] data = new byte[1024];
              InputStream inputStream = socket.getInputStream();
              // 按字节流方式读取数据
              while ((len = inputStream.read(data)) != -1) {
                System.out.println(new String(data, 0, len));
              }
            } catch (IOException e) {
            }
          }).start();

        } catch (IOException e) {
        }

      }
    }).start();
  }
}
```

##### 1.4 总结

在活动连接数不是特别高（小于单机1000）的情况下，这种模型是比较不错的，可以让每一个连接专注于自己的 I/O 并且编程模型简单，也不用过多考虑系统的过载、限流等问题。线程池本身就是一个天然的漏斗，可以缓冲一些系统处理不了的连接或请求。但是，当面对十万甚至百万级连接的时候，传统的 BIO 模型是无能为力的。因此，我们需要一种更高效的 I/O 处理模型来应对更高的并发量。

#### 2. NIO (New I/O)

##### 2.1 NIO 简介

NIO是一种同步非阻塞的I/O模型，在Java 1.4 中引入了 NIO 框架，对应 java.nio 包，提供了 `Channel` , `Selector`，`Buffer` 等抽象。

NIO中的N可以理解为Non-blocking，不单纯是New。它支持面向缓冲的，基于通道的I/O操作方法。 NIO提供了与传统BIO模型中的 `Socket` 和 `ServerSocket` 相对应的 `SocketChannel` 和 `ServerSocketChannel` 两种不同的套接字通道实现,两种通道都支持阻塞和非阻塞两种模式。阻塞模式使用就像传统中的支持一样，比较简单，但是性能和可靠性都不好；非阻塞模式正好与之相反。对于低负载、低并发的应用程序，可以使用同步阻塞I/O来提升开发速率和更好的维护性；对于高负载、高并发的（网络）应用，应使用 NIO 的非阻塞模式来开发。

##### 2.2 NIO的特性/NIO与IO区别

如果是在面试中回答这个问题，我觉得首先肯定要从 NIO 流是非阻塞 IO 而 IO 流是阻塞 IO 说起。然后，可以从 NIO 的3个核心组件/特性为 NIO 带来的一些改进来分析。如果，你把这些都回答上了我觉得你对于 NIO 就有了更为深入一点的认识，面试官问到你这个问题，你也能很轻松的回答上来了。

1)Non-blocking IO（非阻塞IO）

**IO流是阻塞的，NIO流是不阻塞的。**

Java NIO使我们可以进行非阻塞IO操作。比如说，单线程中从通道读取数据到buffer，同时可以继续做别的事情，当数据读取到buffer中后，线程再继续处理数据。写数据也是一样的。另外，非阻塞写也是如此。一个线程请求写入一些数据到某通道，但不需要等待它完全写入，这个线程同时可以去做别的事情。

Java IO的各种流是阻塞的。这意味着，当一个线程调用 `read()` 或  `write()` 时，该线程被阻塞，直到有一些数据被读取，或数据完全写入。该线程在此期间不能再干任何事情了

2)Buffer(缓冲区)

**IO 面向流(Stream oriented)，而 NIO 面向缓冲区(Buffer oriented)。**

Buffer是一个对象，它包含一些要写入或者要读出的数据。在NIO类库中加入Buffer对象，体现了新库与原I/O的一个重要区别。在面向流的I/O中, 可以将数据直接写入或者将数据直接读到 Stream 对象中。虽然 Stream 中也有 Buffer 开头的扩展类，但只是流的包装类，还是从流读到缓冲区，而 NIO 却是直接读到 Buffer 中进行操作。

在NIO厍中，所有数据都是用缓冲区处理的。在读取数据时，它是直接读到缓冲区中的; 在写入数据时，写入到缓冲区中。任何时候访问NIO中的数据，都是通过缓冲区进行操作。

最常用的缓冲区是 ByteBuffer,一个 ByteBuffer 提供了一组功能用于操作 byte 数组。除了ByteBuffer,还有其他的一些缓冲区，事实上，每一种Java基本类型（除了Boolean类型）都对应有一种缓冲区。

3)Channel (通道)

NIO 通过Channel（通道） 进行读写。

通道是双向的，可读也可写，而流的读写是单向的。无论读写，通道只能和Buffer交互。因为 Buffer，通道可以异步地读写。

4)Selector (选择器)

NIO有选择器，而IO没有。

选择器用于使用**单个线程处理多个通道**。因此，它需要较少的线程来处理这些通道。线程之间的切换对于操作系统来说是昂贵的。 因此，为了提高系统效率选择器是有用的。

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161552699.png" alt="image-20210119161552699" style="zoom:60%;" />


##### 2.3  NIO 读数据和写数据方式

通常来说NIO中的所有IO都是从 Channel（通道） 开始的。

- 从通道进行数据读取 ：创建一个缓冲区，然后请求通道读取数据。
- 从通道进行数据写入 ：创建一个缓冲区，填充数据，并要求通道写入数据。

数据读取和写入操作图示：

<img src="C:\Users\lizengcai\AppData\Roaming\Typora\typora-user-images\image-20210119161610061.png" alt="image-20210119161610061" style="zoom:50%;" />


##### 2.4 NIO核心组件简单介绍

NIO 包含下面几个核心的组件：

- Channel(通道)
- Buffer(缓冲区)
- Selector(选择器)

整个NIO体系包含的类远远不止这三个，只能说这三个是NIO体系的“核心API”。我们上面已经对这三个概念进行了基本的阐述，这里就不多做解释了。

##### 2.5 代码示例

代码示例出自闪电侠的博客，原地址如下：        

[https://www.jianshu.com/p/a4e03835921a](https://www.jianshu.com/p/a4e03835921a)

客户端 IOClient.java 的代码不变，我们对服务端使用 NIO 进行改造。以下代码较多而且逻辑比较复杂，大家看看就好。

```java
public class NIOServer {
    public static void main(String[] args) throws IOException {
        // 1. serverSelector 负责轮询是否有新的连接，服务端监测到新的连接之后，不再创建一个新的线程，
        // 而是直接将新连接绑定到clientSelector上，这样就不用 IO 模型中 1w 个 while 循环在死等
        Selector serverSelector = Selector.open();
        // 2. clientSelector 负责轮询连接是否有数据可读
        Selector clientSelector = Selector.open();
        new Thread(() -> {
            try {
                // 对应IO编程中服务端启动，监听socket端口的多个socket连接
                ServerSocketChannel listenerChannel = ServerSocketChannel.open();
                listenerChannel.socket().bind(new InetSocketAddress(3333));
                listenerChannel.configureBlocking(false);
                listenerChannel.register(serverSelector, SelectionKey.OP_ACCEPT);

                while (true) {
                    // 监测是否有新的连接，这里的1指的是 select 阻塞的时间为 1ms
                    //大于0 表示某个socket连接所需的数据准备好
                    if (serverSelector.select(1) > 0) {
                        Set<SelectionKey> set = serverSelector.selectedKeys();
                        Iterator<SelectionKey> keyIterator = set.iterator();

                        while (keyIterator.hasNext()) {
                            SelectionKey key = keyIterator.next();
                            //再次判断当前socket连接是否可读(所需的数据准备好)
                            if (key.isAcceptable()) {
                                try {
                                    // (1) 每来一个可读的新连接，不需要创建一个线程，而是直接注册到clientSelector
                                    SocketChannel clientChannel = ((ServerSocketChannel) key.channel()).accept();
                                    clientChannel.configureBlocking(false);
                                    clientChannel.register(clientSelector, SelectionKey.OP_READ);
                                } finally {
                                    keyIterator.remove();
                                }
                            }

                        }
                    }
                }
            } catch (IOException ignored) {
            }
        }).start();
        //第二个线程使用IO多路复用+非阻塞IO去读取数据，对每个IO无需创建一个新的线程
        new Thread(() -> {
            try {
                while (true) {
                    // (2) 批量轮询是否有哪些连接有数据可读，这里的1指的是阻塞的时间为 1ms
                    if (clientSelector.select(1) > 0) {
                        Set<SelectionKey> set = clientSelector.selectedKeys();
                        Iterator<SelectionKey> keyIterator = set.iterator();

                        while (keyIterator.hasNext()) {
                            SelectionKey key = keyIterator.next();

                            if (key.isReadable()) {
                                try {
                                    SocketChannel clientChannel = (SocketChannel) key.channel();
                                    ByteBuffer byteBuffer = ByteBuffer.allocate(1024);
                                    // (3) 面向 Buffer
                                    clientChannel.read(byteBuffer);
                                    byteBuffer.flip();
                                    System.out.println(Charset.defaultCharset().newDecoder().decode(byteBuffer).toString());
                                } finally {
                                    keyIterator.remove();
                                    key.interestOps(SelectionKey.OP_READ);
                                }
                            }

                        }
                    }
                }
            } catch (IOException ignored) {
            }
        }).start();

    }
}

```

为什么大家都不愿意用 JDK 原生 NIO 进行开发呢？从上面的代码中大家都可以看出来，是真的难用！除了编程复杂、编程模型难之外，它还有以下让人诟病的问题：

- JDK 的 NIO 底层由 `epoll` 实现，该实现饱受诟病的空轮询 bug 会导致 cpu 飙升 100%
- 项目庞大之后，自行实现的 NIO 很容易出现各类 bug，维护成本较高，上面这一坨代码我都不能保证没有 bug

Netty 的出现很大程度上改善了 JDK 原生 NIO 所存在的一些让人难以忍受的问题。

#### 3. AIO (Asynchronous I/O)

AIO 也就是 NIO 2。在 Java 7 中引入了 NIO 的改进版 NIO 2,它是**异步非阻塞**的IO模型。异步 IO 是基于事件和回调机制实现的，也就是应用操作之后会直接返回，不会堵塞在那里，当后台处理完成，操作系统会通知相应的线程进行后续的操作。

AIO 是异步IO的缩写，虽然 NIO 在网络操作中，提供了非阻塞的方法，但是 NIO 的 IO 行为还是同步的。对于 NIO 来说，我们的业务线程是在 IO 操作准备好时，得到通知，接着就由这个线程自行进行 IO 操作，IO操作本身是同步的。（除了 AIO 其他的 IO 类型都是同步的，这一点可以从底层IO线程模型解释，推荐一篇文章：[《漫话：如何给女朋友解释什么是Linux的五种IO模型？》](https://mp.weixin.qq.com/s?__biz=Mzg3MjA4MTExMw==&mid=2247484746&amp;idx=1&amp;sn=c0a7f9129d780786cabfcac0a8aa6bb7&source=41#wechat_redirect) ）

查阅网上相关资料，我发现就目前来说 AIO 的应用还不是很广泛，Netty 之前也尝试使用过 AIO，不过又放弃了。

#### 4. 参考

- 《Netty 权威指南》第二版
- https://zhuanlan.zhihu.com/p/23488863 (美团技术团队)
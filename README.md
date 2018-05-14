# SmileDemo
## 1.java中==和equals和hashCode的区别

相关博客：https://www.cnblogs.com/kexianting/p/8508207.html
### ==
1.java中的数据类型分为两种，基本数据类型和引用类型；

基本数据类型：byte short char int long float double boolean ，他们之间的比较，使用==，比较的是他们的值

引用数据类型：类 接口 数组，当他们用==进行比较的时候，比较的是他们在内存中的存放地址，所以除非同一个new出来的对象，他们比较后的结果为true，否则结果为false；

2.对象是存放在堆中的，对象的引用（地址）存放在栈中，由此可见，==是对栈中的值进行比较，如果要比较堆中对象的内容是否相同，就要使用equals了

### equqls

1、默认情况（没有覆盖equals方法）下equals方法都是调用Object类的equals方法，而Object的equals方法主要用于判断对象的内存地址引用是不是同一个地址（是不是同一个对象）。

定义的equals与==是等效的

2.要是类中覆盖了equals方法，那么就要根据具体的代码来确定equals方法的作用了，覆盖后一般都是通过对象的内容是否相等来判断对象是否相等。

### hashCode

hashcode方法只有在集合中用到


(1)同一对象上多次调用hashCode()方法，总是返回相同的整型值。

(2)如果a.equals(b)，则一定有a.hashCode() 一定等于 b.hashCode()。 

(3)如果!a.equals(b)，则a.hashCode() 不一定等于 b.hashCode()。此时如果a.hashCode() 总是不等于 b.hashCode()，会提高hashtables的性能。

(4)a.hashCode()==b.hashCode() 则 a.equals(b)可真可假

(5)a.hashCode()！= b.hashCode() 则 a.equals(b)为假。 

“如果两个对象相同，那么他们的hashcode应该相等”，

“如果两个对象不相同，他们的hashcode可能相同”
 
#### 延伸（堆内存和栈内存）
![image](https://img-blog.csdn.net/20151103125937282?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQv/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

1、应用程序所有的部分都使用堆内存，然后栈内存通过一个线程运行来使用。

2、不论对象什么时候创建，他都会存储在堆内存中，栈内存包含它的引用。栈内存只包含本地原始变量和堆中对象变量的引用。

3、存储在堆中的对象是全局可以被访问的，然而栈内存不能被其他线程所访问。

4、栈中的内存管理使用LIFO（后进先出）的方式完成，而堆内存的管理要更复杂了，因为它是全局被访问的。堆内存被分为，年轻一代，老一代等等，更多的细节请看，这篇文章

5、栈内存是生命周期很短的，然而堆内存的生命周期从程序的运行开始到运行结束。

6、我们可以使用-Xms和-Xmx JVM选项定义开始的大小和堆内存的最大值，我们可以使用-Xss定义栈的大小

7、当栈内存满的时候，Java抛出java.lang.StackOverFlowError异常而堆内存满的时候抛出java.lang.OutOfMemoryError: Java Heap Space错误

8、和堆内存比，栈内存要小的多，因为明确使用了内存分配规则（LIFO），和堆内存相比栈内存非常快。



## 2.int、char、long各占多少字节数

byte---short--int --long

boolean---char---float---double

1byte(字节)---2byte---4byte---8byte

8bits(位)---16bits---32bits---64bits

## 3.int与integer的区别
1.Integer是int提供的封装类，而int是java的基本数据类型

2.Integer的默认值是null，而int的默认值是0

3.声明为Integer的变量需要实例化，而声明为int的变量不需要实例化

4.Integer是对象，用一个引用指向这个对象，而int是基本类型，直接存储数值


## 4.谈谈对java多态的理解

多态存在的三个前提条件：

1.要有继承关系

2.子类要重写父类的方法

3.父类的引用指向子类的对象

eg ：Animal animal = new Cat（）；



## 5.String、StringBuffer、StringBuilder区别

String 字符串常量

StringBuffer 字符串变量（线程安全）

StringBuilder 字符串变量（非线程安全）


## 6.什么是内部类？内部类的作用

1.内部类（ Inner Class ）就是定义在另外一个类里面的类。与之对应，包含内部类的类被称为外部类。分为以下四种：

成员内部类:类似于成员变量

静态内部类：使用static修饰的内部类

方法内部类：在外部类方法中定义的类

匿名内部类：类似android中的click点击事件，是一种没有构造器的类


 内部类的作用：

1.内部类提供了更好的封装，可以把内部类隐藏在外部类之内，不允许同一个包中其他类访问该类

2.内部类的方法可以直接访问外部类的所有数据，包括私有的数据

3.内部了所实现的功能使用外部类同样可以实现，只是有时候使用内部类更方便



```
// 静态内部类与非静态内部类
static class Outer {
	class Inner {}
	static class StaticInner {}
}

Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
Outer.StaticInner inner0 = new Outer.StaticInner();
```

## 7.抽象类和接口区别

![image](https://img-blog.csdn.net/20170127115356343?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvSGhjMDkxNw==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

原则一：static永远不能和abstract碰头； 

原则二：interface是更抽象的抽象类，接口的所有方法都未实现，接口的方法默认为public abstract ，根据原则一，当然不能是static了； 

原则三：抽象类是部分实现的，其中non－abstract方法可以带static，abstract方法不能带static；


## 8.抽象类的意义

抽象类的意义：

1，为子类提供一个公共的类型；

2，封装子类中重复内容（成员变量和方法）；

3，定义有抽象方法，子类虽然有不同的实现，但该方法的定义是一致的。


![image](https://img-blog.csdn.net/20170212210633170?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvY3Jhenlfa2lkX2huZg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/Center)

## 9.抽象类与接口的应用场景

abstract class的应用场合

一句话，在既需要统一的接口，又需要实例变量或缺省的方法的情况下，就可以使用它。最常见的有：

 A. 定义了一组接口，但又不想强迫每个实现类都必须实现所有的接口。可以用abstract class定义一组方法体，甚至可以是空方法体，然后由子类选择自己所感兴趣的方法来覆盖。
 
 B. 某些场合下，只靠纯粹的接口不能满足类与类之间的协调，还必需类中表示状态的变量来区别不同的关系。abstract的中介作用可以很好地满足这一点。
 
 C. 规范了一组相互协调的方法，其中一些方法是共同的，与状态无关的，可以共享的，无需子类分别实现；而另一些方法却需要各个子类根据自己特定的状态来实现特定的功能



其他情况下都是使用 接口。

## 10.抽象类是否可以没有方法和属性？

可以

## 11.接口的意义

1.有利于代码规范

2.有利于对代码进行维护

3.保证代码的安全和严密

## 12.泛型中extends和super的区别

<? extends T> 表示上界通配符 它表示T以及T的子类， 类型最高是T

<? super T> 表示下界通配符 它表示T以及T的超类，类型最高可到Object ，最低是T

<? extends T> 不能存数据，但是可以取数据

<? super T> 下界通配符： 表示T以及T的超类，可以存数据，但是只能取出Object的数据


## 13.父类的静态方法能否被子类重写
java中静态属性和静态方法可以被继承，但是没有被重写(overwrite)而是被隐藏.

## 14.进程和线程的区别
一个程序至少有一个进程,一个进程至少有一个线程.

## 15.final，finally，finalize的区别


final 用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，类不可继承。

finally是异常处理语句结构的一部分，表示总是执行。

finalize是Object类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，可以覆盖此方法提供垃圾收集时的其他资源回收，例如关闭文件等。



## 16.android序列化的方式
Serializable

Parcelable


## 17.Serializable 和Parcelable 的区别


区别| Serializable|Parcelable 
---|---|---
所属API |JAVA API|Android SDK API
原理 | 序列化和反序列化过程需要大量的I/O操作|序列化和反序列化过程不需要大量的I/O操作
开销|开销大|开销小
效率|低|很高
使用场景 |序列化到本地或者通过网络传输|内存序列化


## 18.静态属性和静态方法是否可以被继承？是否可以被重写？以及原因？

java中静态属性和静态方法可以被继承，但是没有被重写(overwrite)而是被隐藏.

原因：

1). 静态方法和属性是属于类的，调用的时候直接通过类名.方法名完成对，不需要继承机制及可以调用。如果子类里面定义了静态方法和属性，那么这时候父类的静态方法或属性称之为"隐藏"。如果你想要调用父类的静态方法和属性，直接通过父类名.方法或变量名完成，至于是否继承一说，子类是有继承静态方法和属性，但是跟实例方法和属性不太一样，存在"隐藏"的这种情况。

2). 多态之所以能够实现依赖于继承、接口和重写、重载（继承和重写最为关键）。有了继承和重写就可以实现父类的引用指向不同子类的对象。重写的功能是："重写"后子类的优先级要高于父类的优先级，但是“隐藏”是没有这个优先级之分的。

3). 静态属性、静态方法和非静态的属性都可以被继承和隐藏而不能被重写，因此不能实现多态，不能实现父类的引用可以指向不同子类的对象。非静态方法可以被继承和重写，因此可以实现多态。

## 19.静态内部类的设计意图
## 20.成员内部类、静态内部类、局部内部类和匿名内部类的理解，以及项目中的应用

### 相关博客：http://www.cnblogs.com/latter/p/5665015.html

#### 20.1成员内部类:

1.类似于成员变量

2.成员内部类可以无条件访问外部类的所有成员属性和成员方法（包括private成员和静态成员）。

3.不过要注意的是，当成员内部类拥有和外部类同名的成员变量或者方法时，会发生隐藏现象，即默认情况下访问的是成员内部类的成员。如果要访问外部类的同名成员，需要以下面的形式进行访问：

外部类.this.成员变量

外部类.this.成员方法

4.虽然成员内部类可以无条件地访问外部类的成员，而外部类想访问成员内部类的成员却不是这么随心所欲了。在外部类中如果要访问成员内部类的成员，必须先创建一个成员内部类的对象，再通过指向这个对象的引用来访问：

5.成员内部类是依附外部类而存在的，也就是说，如果要创建成员内部类的对象，前提是必须存在一个外部类的对象。

6.内部类可以拥有private访问权限、protected访问权限、public访问权限及包访问权限。


#### 20.2方法内部类（局部内部类）：在外部类方法中定义的类

局部内部类就像是方法里面的一个局部变量一样，是不能有public、protected、private以及static修饰符的


#### 20.3匿名内部类：类似android中的click点击事件，是一种没有构造器的类

匿名内部类是唯一一种没有构造器的类


#### 20.4静态内部类：使用static修饰的内部类

静态内部类是不需要依赖于外部类的，这点和类的静态成员属性有点类似，并且它不能使用外部类的非static成员变量或者方法

## 21.谈谈对kotlin的理解
## 22.闭包和局部内部类的区别
## 23.string 转换成 integer的方式及原理
### String转Integer

当我们要把String转化为Integer时，一定要对String进行非空判断，否则很可能报空指针异常。


```
String str = "...";
Integer i = null;
if(str!=null){
     i = Integer.valueOf(str);
}

```

### Integer转String

//方法一:Integer类的静态方法toString()

Integer a = 2;
String str = Integer.toString(a)

//方法二:Integer类的成员方法toString()

Integer a = 2;
String str = a.toString();

//方法三:String类的静态方法valueOf()

Integer a = 2;
String str = String.valueOf(a);

## 24.public private  protect  default 的区别

  名称 | 同一个类|同一个包|不同包的子类|不同包的非子类
---|---|---|---|---
private | √ |   |   |  
default | √ |√ |   |  
protect | √  | √  |  √ |  
public |  √ | √ |  √ | √

public： Java语言中访问限制最宽的修饰符，一般称之为“公共的”。被其修饰的类、属性以及方法不仅可以跨类访问，而且允许跨包（package）访问。

private: Java语言中对访问权限限制的最窄的修饰符，一般称之为“私有的”。被其修饰的类、属性以及方法只能被该类的对象访问，其子类不能访问，更不能允许跨包访问。

protect: 介于public 和 private之间的一种访问修饰符，一般称之为“保护形”。被其修饰的类、属性以及方法只能被类本身的方法及子类访问，即使子类在不同的包中也可以访问。

default：即不加任何访问修饰符，通常称为“默认访问模式“。该模式下，只允许在同一个包中进行访
　　　　　问。


    作者：AWeiLoveAndroid
    链接：https://www.jianshu.com/p/c70989bd5f29
    來源：简书
    著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

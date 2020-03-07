---
title: JAVA题目
date: 2019-10-09 15:47:45
categories: "JAVA" 
tags: JAVA
description: JAVA题目



---

### 1. private修饰的方法可通过反射访问，那么private的意义是什么？

> 可以修饰成员变量和成员方法，如果类的成员被private访问控制符修饰，则这个成员只能被该类的其他成员访问，其他类无法直接访问。类的良好封装就是通过private关键字实现的。
>
> 但是俗话说没有不透风的墙。我们可以利用java中的反射从而在外界调用private的变量或方法
>
> 不是为了绝对安全性设计的，是用来约束用户常规使用JAVA的方式。这就像是一家没人的店挂了个牌子“闲人免进”，但你真要进去还是有各种办法可以办到。所以private，以及所有其他的access modifier都有一层隐含的含义：如果你按照遵守这套规则，开发者可以保证不出问题（不考虑bug的情况下）；否则，后果自负。
>
> 

```java
package PrivateTest;

public class PrivateCar {
    
	//private成员变量：在传统的类实例调用方式，只能在本类中访问
	private String color="黄色";
    
	//protected方法：使用传统的类实例调用方式，只能在子类和本包中访问
	protected void drive() {
		System.out.println("this is private car! the color is:" + color);
	}
 	public static void main(String[] args) throws Throwable {
		PrivateCar pcar = new PrivateCar();
		pcar.drive();
	}
}

//返回结果：（this is private car! the color is:黄色）
```

```java
package PrivateTest;

import java.lang.reflect.Field;

public class PrivateCarReflect {
	public static void main(String[] args) throws Throwable {
		Class clazz = PrivateCar.class;
		PrivateCar pcar = (PrivateCar) clazz.newInstance();

		Field colorFld = clazz.getDeclaredField("color");
		//取消java语言访问检查以访问private变量
		colorFld.setAccessible(true);
		colorFld.set(pcar, "红色");
		pcar.drive();
	}
}

//返回结果：（this is private car! the color is:红色）
```

### 2.一个java文件有三个类，编译后有几个class文件？

> 3个。有几个类就产生几个class文件。

### 3.局部变量使用前要显式地赋值，否则编译不通过，为什么这样设计？

> 成员变量不用显式赋值，在类加载的过程中给它赋予了默认值。
>  局部变量需要显式赋值。
>  **为啥不给它赋予默认值？**
>  不是javac推断不出来，而是因为推断出来了，故意不这么做。
>  **为啥故意不这么做？**
>  因为局部变量的作用就是在局部方法中某个地方取出来用。在一个方法体内赋值和取值的顺序是固定，先赋值，才能取值。强制你赋值时因为怕你忘了！怕有了默认值之后忘记赋值导致不可预期的bug！
>  **那为啥成员变量有了默认值不怕有bug？**
>  因为成员变量不确定什么就会被取值出来用，还有可能在各个方法中是不同的值。所以强制让你赋值和给它默认值没什么区别，既然这样，为什么不默认呢?
>
> <https://blog.csdn.net/x2L5gX/article/details/81090855>

### 4.什么叫原子性操作？int i= 1 是原子性操作吗？

> 所谓原子操作是指不会被线程调度机制打断的操作；这种操作一旦开始，就一直运行到结束，中间不会有任何 context switch （切换到另一个线程）。原子操作是不可分割的，在执行完毕之前不会被任何其它任务或事件中断。在单处理器系统中，能够在单条指令中完成的操作都可以认为是" 原子操作"，因为中断只能发生于指令之间。
>
> 通常所说的原子操作包括对非long和double型的primitive进行赋值，以及返回这两者之外的primitive。之所以要把它们排除在外是因为它们都比较大，而JVM的设计规范又没有要求读操作和赋值操作必须是原子操作。(Primitive JAVA的8个基本类型：boolean，char，byte，short，int，long，float，double)
>
> int i= 1 是原子性操作。

### 5.接口不用public修饰，实现类要public修饰

     如果接口不是public，那么只能在同个包下被实现，可访问权限就降低很多了。
接口中的方法隐含都是public和abstrac。


 而java类中成员缺省的修饰符是不写修饰符，理解为friendly(default)，拥有的权限是包权限，子类不写public时访问权限较低。

### 6.String之所以不可变，是因为jdk中用final修饰了它。

![final变量修饰String类](https://www.qisuiyi.top/img/Final+String.png "String类不可变的原因")

  <div STYLE="page-break-after: always;"></div>  
### 7.final修饰符：

-   修饰类

    -   final类不能被继承。

    -   final类中的成员方法都会被隐式的指定为final方法

    -   final类中的成员变量可以根据自己的实际需要设计为final

    -   JDK中，被设计为final类的有String、System等。

-   修饰方法

    -   final方法不能被重写

    -   一个类的private方法会隐式的被指定为final方法。

-   修饰成员变量

    -   必须要赋初始值，而且是只能初始化一次。

    -   如果修饰的成员变量是基本类型，则表示这个变量的值不能改变

    -   如果修饰的成员变量是一个引用类型，则是说这个引用的地址的值不能修改，但是这个引用所指向的对象里面的内容还是可以改变的。

### 8.static修饰符：

-   修饰变量：

    -   静态变量在内存中只有一份

    -   可以直接通过类名访问。

-   修饰方法

    -   必须有实现即不能是抽象方法

    -   只能访问所属类中的静态字段和静态方法。

-   静态导包

//使用静态变量和方法不用再指明classname，从而简化代码。（降低了可读性）

```java
import static com.xxx.ClassName.*
```



### 9.成员变量与局部变量

-   成员变量

    -   存在于对象所在的堆内存中。

    -   有默认初始值。

-   局部变量

    -   存在于栈内存中。

    -   没有默认初始化值。

### 10.反射

![反射](https://www.qisuiyi.top/img/reflict.png "反射")

-   缺点

    -   开销较大，应避免在经常使用的方法中使用反射。

    -   反射必须在没有安全限制的程序中使用。

    -   造成内部暴露，可能导致意想不到的后果。

    -   破坏了抽象性，在平台改变时，代码行为也可能变化。

### 11.语法糖

- switch（支持string）

  - java文件  

    ```java
    public static void main(String[] args) {
      String str = "world";
      switch (str) {
        case "hello":
          System.out.println("hello");
          break;
        case "world":
          System.out.println("world");
          break;
        default:
          break;
      }
    }
    ```

  - 反编译之后的class文件（实际是对比hash值）

  ```java
  public static void main(String[] args) {
    String str = "world";
    byte var3 = -1;
    switch(str.hashCode()) {
    case 99162322:
      if (str.equals("hello")) {
        var3 = 0;
      }
      break;
    case 113318802:
      if (str.equals("world")) {
        var3 = 1;
      }
    }
    switch(var3) {
    case 0:
      System.out.println("hello");
      break;
    case 1:
      System.out.println("world");
    }
  }
  ```

- 泛型

- 自动装箱/拆箱

  - java

    ```java
    //装箱
    int m = 10;
    Integer n = m;
    
    //拆箱
    Integer i = 10;
    int j = i;
    
    //  class文件
    
    //装箱 通过调用包装器的valueOf方法实现的
    int m = 10;
    Integer n = Integer.valueOf(m);
    
    //拆箱
    Integer i = 10;
    int j = i;
    ```

- 条件编译：不符合条件的代码不编译，

- 数值字面量: 都允许在数字之间插入任意多个下划线，目的为方便阅读。

- for-each:原理为for循环+迭代器

### 12.sys 同步修饰符只能在一台虚拟机用，对于单机系统某些代码可能没问题，多个机器上就会出现问题。

###  13.java缓存池：

 	对于基本类型的变量，如果变量值的范围在缓存池的范围中，就可以直接使用缓冲池中的对象。

    基本类型对应的缓冲池如下：

-   boolean ： true and false

-   byte：all byte values

-   short ： -128 - 127

-   int ：  -128 - 127（  IntegerCache 很特殊可以通过参数调节 ，启动 jvm
    的时候，通过 -XX:AutoBoxCacheMax=\<size\> 来指定这个缓冲池的大小）

-   char ：\\u0000 - \\u007F

//valueOf()就是利用缓存池的例子，调用时会先判断值是否在缓存池中，如果在的话就直接返回缓存池的内容。

```java
public static Integer valueOf(int i) {
     if (i \>= IntegerCache.low && i \<= IntegerCache.high)
         return IntegerCache.cache[i + (-IntegerCache.low)]; 
    return new Integer(i); 
}
```

### 14.强转

1. 字符串转换成整数（ 字符串转换成byte, short, int, float, double,
   long等数据类型，可以分别参考Byte, Short, Integer, Float, Double,
   Long类的parseXXX方法。）

   ```java
   String MyNumber ="1234";
   int MyInt = Integer.parseInt(MyNumber);
   ```

   2. 整数转换成字符串：

      ```java
      int MyInt = 1234;
      String MyString = "" + MyInt;
      ```

### 15.jdk8的optional

- ofNullable()/of()：初始化

- isPresent()：判断是否有值

  ```java
  String name = null;
  Optional<String> opt1 = Optional.of(name);//报错：NullPointerException
  Optional<String> opt2 = Optional.of(name);//opt2=Optional.empty
  System.out.println(opt1.isPresent());//false
  ```

- orElse();

- orElseGet();

  ```java
  public static void main(String[] args) {
    String name = null;
    System.out.println("orElse:");
    String str1 = Optional.ofNullable(name).orElse(getName());
    System.out.println(str1);
    System.out.println("orElseGet:");
    String str2 = Optional.ofNullable(name).orElseGet(()-\>getName());
    System.out.println(str2);
  }
  
  private static String getName() {
    System.out.println("调用getName方法");
    return "xiaoming";
  }
  
  //name为null时，输出结果为
  //orElse:   调用getName方法  xiaoming
  //orElseGet: 调用getName方法  xiaoming
  
  //name为："xiaogang"时，输出结果为
  //orElse:      调用getName方法  xiaogang 
  //orElseGet:   xiaogang
  
  ```



差异为 入参为null时，orElse()方法会调用里面的方法，但是必须返回string.在执行较密集的调用时，比如调用 Web
服务或数据查询，**这个差异会对性能产生重大影响**。

- .filter()方法，按条件筛选。可以用来筛选邮箱、中英文字符密码等。

  ```java
  String str1 ="[aa163.com";](http://aa163.com/)
  String result =Optional.ofNullable(str1).filter(u -\> u!= null &&u.contains("\@")).orElse("<bb@163.com>");
  
  
  ```

  


## Java应用技术1：基础语法

###### RandomStar

##### 成绩组成

- 平时分70%+期末考试30%
  - 包含出勤，PTA作业，编程小作业，大作业，期中考试



#### Chapter 1：Introduction

##### 1.1 Java语言的特性

- 简洁
  - 没有C/C++中的指针，没有多重继承和运算符重载的语法特性
- 面向对象
  - Java设计的核心是如何复用代码，并且支持继承封装多态
- Interpreted
  - 代码会编译成字节码(bytecode)在Java虚拟机上运行
  - Java是跨平台的，可以在所有有JVM的计算机上运行，JMV可以设置不同的安全等级
- 鲁棒性
  - 强类型机制，异常处理，垃圾内存自动搜集等机制

##### 1.2 JDK的版本

- Java Standard Edition (J2SE)
  - 可以用于开发客户端应用和app
- Java Enterprise Edition (J2EE)
  - 可以用于开发服务端应用，比如Java Servlets
- Java Micro Edition (J2ME)
  - 开发手机应用
- 本课程中的内容主要是**J2SE** 

##### 1.3 Java程序的组成

- 一个简单的Java程序

```java
public class HelloWorld{
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

- Java代码编译的过程
  - Java代码文件的后缀名是`.java`，被Java编译器编译之后编译成`.class`文件，之后在JVM中运行
- 每个Java程序至少需要一个class，每个class都有唯一的class name
  - block是java程序的组件，比如一个类就是一个class block
- Java程序中的错误
  - 语法错误Syntax Error：会在编译期间被检查出来，因此有语法错误的时候无法通过编译
  - 运行时错误 Run time Error：
  - 程序逻辑上本身的错误

##### ⭐作业里一道莫名其妙的题目

- 对于下面的这样一个Java程序，它**可以通过编译**但是运行的时候会因为**没有入口main函数**而出现错误
  - 这是因为Java的编译器会把类编译成class文件，下面这个类是一个合法的类，没有语法错误，因此可以通过编译
  - 但是在JVM中执行的时候会因为没有入口main函数而出现错误

```Java
public class main {
    public void main() {
        System.out.println("Hello World!");
    }
}
```



#### 2. Java的基本语法

##### 2.1 Java的变量命名

- 变量：包含大小写字母，数字，下划线和$符号

  - Java中的变量不能用数字开头，也不能是保留字

- 变量的定义和声明

  - Java中**不区分变量的声明和定义**，这是和C/C++的最大不同
    - C/C++中的编译器**不会为基本类型赋予初始默认值**
  - Java对于方法的局部变量，Java以**编译时错误**来保证**变量在使用前都能得到恰当的初始化 ** 
    - 但是Java对于方法内的单个变量不会赋予初始值，对于数组会赋予默认的值
  
- 对于下面这样一段代码
  
  - 输出的结果是0，因为**变量进行了初始化但是没有赋予具体值**
  - Java中int类型的默认值就是0
  
  ```Java
  public class JavaPractice {
      static int array[] = new int[5];
      public static void main(String a[]) {
          System.out.println(array[0]);
      }
  }
  ```
  
- **常量**定义`final datatype CONSTANTNAME = VALUE;`
    - final的主要用法有如下三种
      - 修饰变量，表示变量的值**不能改变**，但是可以进行任何合法形式的初始化，相当于C/C++中的const类型
        - 修饰类对象，表示这个变量不能再赋值成其他的对象，比如一个对象被new了之后，就不能再把它new成一个新的对象
      - 修饰方法method，表示一个Java函数不可更改，**不能被重载** 
      - 修饰类，表示这个类**不能被继承**，类中的所有方法也就变成了final类型的
  
- Java中的变量类型

  - 数值型变量：Java中整数类型的范围和**运行的机器无关**，这一点和C/C++不同
    - byte 8bit 有符号类型
    - short 16bit 有符号类型
    - int 32bit有符号类型
    - long 64bit有符号类型
    - float和double分别是32bit和64bit的IEEE754标准
  - **字符类型char** 
    - 编码方式是Unicode
    - Java中的一个char类型变量占16bits，也就是2个字节

- 数值类型的读入

  - 首先需要定义Scanner读入器`Scanner input = new Scanner(System.in)`
  - 之后可以用input的`nextInt`方法读取下一个整数，其他数据类型同理

- Java中的数值运算：支持加减乘除取余等各种操作

  - 除法中如整数除法的结果是整数，浮点数除法的结果浮点数

  - 浮点数中double比float更加精确，double精确到16位，float精确到8位小数
  - 几个特殊的浮点数值
    - `Double.POSITIVE_INFINITY` 正无穷大
    - `Double.NEGATIVE_INFINITY` 负无穷大
    - `Double.NaN` 不是数字
    - 可以用Double.isNaN来判断是否为数字

- 类型转换：byte，short，int，float，double，long，char之间可以进行类型转换

  - 其中整形向浮点型的转换可能会造成精度的损失
  - 浮点数向整形转换的时候会丢弃小数部分
  - Java不支持C++中的自动强制类型转换，有需要的类型转换必须显式地声明

##### 2.2 选择语句

- 布尔类型变量(boolean) 值只有true和false，Java中的大小关系符和C/C++一致

###### 2.2.1 if语句和switch语句

- 和C/C++基本一致，没啥好学的

- if语句有单个if，if-else，多层嵌套if等写法，**else和最近的if匹配** 

- switch语句也跟C/C++基本一致，有break有default

  - 布尔类型不能用在switch的选择里，下面的代码是错误的

  ```Java
  boolean x;
  switch(x) {
  	// 
  }
  ```

###### 2.2.2 逻辑运算符

- Java中有如下逻辑运算符

  - ！逻辑否，&&逻辑且，|| 逻辑或，**^逻辑异或** 
  - &&和||的运算按照短路的方式来求值，如果第一个操作数已经可以确定表达式的值，后面的就不需要进行运算了
  - &和|也可以进行逻辑运算，区别是这两个不用短路的方式来求值

  <img src="C:\Users\74096\AppData\Roaming\Typora\typora-user-images\image-20200708231822126.png" alt="image-20200708231822126" style="zoom:67%;" />

##### 2.3 数学函数

- 常见的两个常数：PI和E表示圆周率和自然对数的底数
- 常见的数学类方法
  - 三角函数
  - 幂
  - 高斯函数和舍入方法
  - 最大，最小，绝对值和随机

##### 2.4 字符和字符串类型

- Java中的字符类型有两种表示方式，ASCII编码和Unicode编码模式
  - Unicode编码模式的形式是前缀`\u`+四位十六进制数，可以表示从0000到FFFF一共65536个字符
  - 常见的ASCII码
    - '0' - '9'在ASCII码中式48到57
    - 'A' - 'Z' 式65-90， 'a'-'z'是97-122
- 字符串内置方法

![image-20200709172718342](C:\Users\74096\AppData\Roaming\Typora\typora-user-images\image-20200709172718342.png)

- 字符串类型 String

  - 一些简单的内置方法

  ![image-20200709174536954](C:\Users\74096\AppData\Roaming\Typora\typora-user-images\image-20200709174536954.png)

  ![image-20200709175413874](C:\Users\74096\AppData\Roaming\Typora\typora-user-images\image-20200709175413874.png)

  - 读取字符串的方式：
    - 使用next() 从有效字符开始扫描，遇到第一个分隔符或者结束符的时候结束，将结果作为字符串返回
    - nextLine扫描当前行所有的字符串作为结果返回
  - 获取字串，使用`substring`方法，必须要有的参数是起始位置beginIndex，结束位置endIndex可以缺省，默认值是字符串末尾
  - 访问单个字符和子串的位置

  ![image-20200709175604703](C:\Users\74096\AppData\Roaming\Typora\typora-user-images\image-20200709175604703.png)

  - 字符串类型是不可变的，不能对String中的内容做出改变，同时如果在函数中对String进行赋值操作也不能改变主函数里的String，比如下面这样一段代码，最后的输出还是A,B

  ```java
  public class Main {
      public static void main(String args[]) {
          String a = new String("A");
          String b = new String("B");
          swap(a, b);
          System.out.println(a + "." + b);
      }
      static void swap(String x, String y) {
          y = x;
      }
  }
  ```

  - String的concat和substring等方法都不是在原来的字符串上操作的，而是生成了一个新的字符串

- 格式化输出

  - `System.out.printf(format, items);` 具体的用法和C语言的printf类似

  - 占位符的具体格式包括

    - `%[index$][标识]*[最小宽度][.精度]转换符` 

    - index表示从第几个位置开始计算来进行格式化，起始为1

    - 最小宽度是格式化之后最小的长度，当输出结果小于最小宽度的时候用标识符填补空格，没有标识符的时候用空格填充

      - 字符串可用标识：- 表示左对齐，默认的是右对齐
      - 整数和浮点数可用标识：

      ![image-20200709192611084](C:\Users\74096\AppData\Roaming\Typora\typora-user-images\image-20200709192611084.png)

      - 对日期进行格式化

    - 精度用于设置浮点数保留几位小数

    - 转换符用于指定转化的格式，有f，d等等

##### 2.5 循环

- 和C/C++基本一致，有for循环，while循环和do-while循环
  - 要注意区别while循环和do-while循环
  - `for(;;){}`和`while(true){}`等价
  - Java中也有`break`和`continue`来结束或者跳出循环



##### 2.6 方法

- 将程序中的一部分过程抽象成一个方法，起到代码复用的作用，一个方法的定义包含如下如内容
  - modifier 修饰符，包括方法的public/private/protected和是否是static，final等属性
  - return value type 返回值类型
  - method name 方法名
  - formal parameters 形式参数
    - 方法名+形式参数称为方法的签名
    - 与之相对应的是actual parameter or argument实际参数，也就是调用方法的时候使用的参数
    - 实参的内容不会因为方法中的操作被改变
  - body 方法的具体内容
- 方法的重载：相同的方法名，不同的参数表构成重载关系
  - 只有返回值类型不相同的时候不构成重载，这种写法会引起编译错误，不能使用
  - 重载可以有返回值类型的区别，但是一定会有**参数表的区别** 
- 局部变量：定义在方法内部的变量叫做局部变量
  - 局部变量的可调用范围是从定义开始到不再包含这个变量的方法内部区域为止(比如for循环中定义的变量只能在for循环中调用) 



##### 2.7 数组

###### 2.7.1 一维数组

- Java中数组的定义方式`datatype[ ] array`，中括号也可以放在后面，然后需要用`new datatype[size]`来声明数组的大小

  - 可以用length来获得数组的长度，但要注意这个和String类型的`length()` **方法**不一样，数组里的length是state
  - 数组的长度定义之后就**不能改变** 
  - 数组的长度确定之后，里面所有元素的值会被设定为默认值
    - 对于数值类型的数组，默认值是0
    - 对于char类型，默认值是`\u0000`
    - 对于boolean类型，默认值是false
  - 数组可以在定义的时候直接赋予若干值，此时数组的长度会被自动设定为值的个数，但是下面这种方式是错误的

  ```java
  double[] list;
  list = {1, 2, 3, 4};
  ```

  - Java数组和C++数组的**区别** 
    - Java的数组定义在**堆**上，C++中直接声明大小的数组分配在栈上，动态分配的数组在堆上
    - Java的[ ]运算符被会检查数组边界，防止下标溢出，并且没有指针运算
    - Java中命令行参数是`String[] args`，其中`args[0]`是第一个参数，**程序名没有存储**在args中需要在启动Java程序的时候就输入
  - 数组的遍历
    - 用下标i去遍历一个数组
    - 用`elementType value: arrayRefVar` 的形式来遍历
  - 数组的拷贝：`arraycopy(sourceArray, src_pos, targetArray, tar_pos, length);` 自带的处理方法
    - 在拷贝的过程中，如果被拷贝的数组存在多余的元素，则赋以默认值，如果小于原始数组长度，则只拷贝前面的元素
  - 数组作为方法的参数
    - Anonymous Array 匿名数组：在方法调用中的参数里直接写一个数组，没有用变量去引用，如`new int[]{1,2,3}`直接作为参数
    - 将数组作为参数的时候，数组作为一个引用传入，方法中改变数组的值将会影响到原来的数组，但是匿名数组没有变量名

###### 2.7.2 多维数组

- 二维数组的定义：`dataType[][] refVar;` 
  - 如何new：`new dataType[rowSize][columnSize]` 
  - Java的二维数组每一列大小可以不同，并不需要完全相同！
- 如何创建一个二维数组？以下四种写法中，只有第2行的是对的
  - 总结起来就是中括号可以放在前面也可以放在后面，但是**声明的时候不能直接指定数组的大小**
  - 数组的大小需要在new的时候指定，并且二维数组**一定要有行的数目** 

```Java
int a[3][2] = ;
int a[][] = new int[3][];
int[][] a = new int[][3];
int[][] a = new int[][];
```


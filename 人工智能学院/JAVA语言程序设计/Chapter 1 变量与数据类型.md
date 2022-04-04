#Chapter 1 变量与数据类型
##main函数
```java
public class main {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```
在以上代码中，main是该class的名称。
ATTENTION: Java对类的名称是大小写敏感的。同时，xxx.java的文件名需要与类名相同。

##注释
一段注释用 // 表示，整段注释用 /* */ 表示。

##变量
Java的变量必须指定数据类型。
```java
int n = 0;
String name = "Alice";
```

##数据类型
| Name | Academy | score |
| :- | :- | :- |
| byte | 1 byte | 一个字节 [-128,127] |
| short | 2 bytes | 短整数 [-32768,32767] |
| int | 4 bytes | 整数 [-2,147,483,648, 2,147,483,647] |
| long | 8 bytes| 长整数 [-9,223,372,036,854,775,808, 9,223,372,036,854,775,807] |
| float | 4 bytes | 浮点数 6~7位小数 |
| double | 8 bytes | 浮点数 15位小数 |
| boolean | 1 bit | 布尔值, true或false |
| char | 2 bytes | 单个ASCII字符 |

###常量
对于我们想要固定不允许更改的数值，可以使用常量final.
```java
final int money = 100;
money = 50;
```
此时IDE会提示以下错误：
```java
The final local variable money cannot be assigned. It must be blank and not using a compound assignment
```
我们在以上代码中将50赋值给了常量money.

##类型转换
Java的类型转换包括两种：自动、强制。
**更低位数**的数据可以被自动转换为**更高位数**的数据，反之则需要强制转换。
Java中数据类型从**低位到高位**排序如下。
```java
byte -> short -> char -> int -> long -> float -> double
```
###自动类型转换
```java
char c = 'A';
int n = c;
System.out.println(n);
```
结果为：
```java
65
```
###强制类型转换
```java
double x = 1.5;
int y = (int)x;
System.out.println(y);
```
结果为：
```java
1
```
强制类型转换需要将目标类型加上()写在变量前面。
强制类型转换是直接将小数部分抹去，并不会做四舍五入。

##操作符
操作符分为：
算数、关系、位、逻辑、赋值、其他。
运算符间存在优先级，多为自左向右复合，与一般理解的运算顺序无太大不同。值得注意的是，**单目运算符**和**赋值**是自右向左复合的。
###算术运算符
| 优先级 | 运算符 | 运算 |
| :- | :- | :- |
| 1 | + | 单目取正 |
| 1 | - | 单目取负 |
| 2 | * | 乘法 |
| 2 | / | 除法 |
| 2 | % | 取余 |
| 3 | + | 加法 |
| 3 | - | 减法 |
| 3 | + | 字符串连接 |
| 4 | = | 赋值 |
```java
int a = 0;
int b = 0;
System.out.println("a++ = " + a++);
System.out.println("++b = " + ++b);
System.out.println("a = " + a + "  b = " + b);
```
以上代码运行的结果是：
```java
a++ = 0
++b = 1
a = 1  b = 1
```
值得注意是，a++和++a是不同的操作，虽然它们都将a本身+1了，但是a++和++a两个表达式本身表达的值不同。a++相当于先使用a, 然后再将a+1; 而++a则是先做a+1, 再使用a.

###关系运算符
| 运算符 | 描述 |
| :- | :- |
| == | 相等 |
| != | 不等 |
| > | 大于 |
| < | 小于 |
| >= | 大于或等于 |
| <= | 小于或等于 |
关系运算的结果是布尔值。超过一个字符的关系运算符中间是不能有空格的，例如，">="不能写成"> =".

###逻辑运算符
| 运算符 | 描述 |
| :- | :- |
| && | 短路与 |
| &#124;&#124; | 短路或 |
| ! | 逻辑非 |

##数组
Java中的数组存储多个相同数据类型的数值。
###一维数组
按照以下形式创建数组。
```java
<类型>[]<名称> = new <类型>[元素个数];
int[] numbers = new int[3]
```
或者，可以直接初始化数组。
```java
int[] numbers = {0,1,2};
String[] name = {"Alice","Bob","David"};
```
对数组内所有内容的输出一般都使用for循环遍历整个数组。数组有方法length, 可以返回数组的长度。
```java
int[] numbers = new int[3];
numbers[0] = 1;
for ( i = 0; i < numbers.length; i++ ) {
    System.out.print(numbers[i]+"\t");
}
```
以上代码运行结果为：
```java
1       0       0
```
通过以上代码，我们还可以看出，没有赋值的数组元素为0.

###二维数组
```java
int[][] numbers = new int[3][5]
```
以上代码表示创建了一个**3行5列**的数组。
```java
for ( i=0; i<3; i++ ) {
    for ( j=0; j<5; j++ ) {
        a[i][j] = i*j;
    }
}
```
通过以上代码即可遍历该二维数组。
```java
int[][] a = {
    {1,2,3,4},
    {1,2,3},
};
```
通过以上代码创建了一个二维数组，编译器可以自动数出行数和列数。省略的数会被补0.

##字符类型
###char类型
```java
char letter0 = 65;
char letter1 = 'A';
System.out.println(letter0);
System.out.println(letter1);
```
以上代码运行结果是：
```
A
A
```
对char类型的赋值既可以用ASCII码也可以用字符。但是，字符的引号是单引号，不能使用双引号。若使用双引号，会提示以下错误信息：
```java
Type mismatch: cannot convert from String to char
```
这里可以看出，Java双引号内为String类型。

###字符串String
我们应该已经见过String的初始化，可能注意到，String并不是前述的几种数据类型之一。实际上，String是一个内置的类，它具有一些可供调用的方法。
可以使用
```java
String s = new String("a string");
```
来创建一个新字符串。
使用
```java
String s = "Hello!";
```
来初始化一个字符串。
值得注意的是，所有的字符串都是不可变的。对字符串的操作会制造新的字符串，而不是改变原字符串。例如：
```java
String s = "abc";
System.out.println(s.toUpperCase());
System.out.println(s);
```
结果为：
```java
ABC
abc
```

####字符串连接
用加号+即可连接字符串。
```java
"hello"+"world"->"hello world"
```

####输入字符串
```java
in.next();
```
读入一个单词，以空格为标志。此处空格包括空格、tab、换行符。
```java
in.nextLine();
```
读入一整行。

####相等关系
字符串不能使用==来比较，应当使用.equals比较。
```java
input.equals("bye");
```

####比大小(.compareTo方法)
该方法返回值是整形。它比较两个字符串相对应位置字符的大小（ASCII码），如果第0个字符不等，结束比较，返回长度**差值**。如果相等，则比较到不相等为止。如果相等，则返回0. 例如：
```java
String s1 = "Strings";
String s2 = "Strings";
String s3 = "Strings123";

int result = s1.compareTo(s2);
System.out.print(result + "\t");

result = s2.compareTo(s3);
System.out.print(result + "\t");

result = s3.compareTo(s1);
System.out.print(result);
```
以上代码运行的结果为：
```java
0       -3      3
```

####获得字符串长度(.length方法)
```java
String str1 = "Hello";
System.out.println(str1.length());
```
结果为：
```java
5
```

####访问String里的字符(.charAt方法)
```java
s.charAt(index);
```
返回index索引上的单个字符，index的范围是[0,length()-1].

####获得子串(.substring方法)
```java
s.substring(a,b);   //得到index为a到e之间的所有内容
s.substring(a);     //得到index为a到末尾的所有内容
```

####寻找字符
```java
s.indexOf(c);   //得到c字符的位置，-1表示不存在
s.indexOf(c,n); //同上，从n号开始找
s.indexOf(t);   //找字符串t的位置
//从右边找
s.lastIndexOf(c);
s.lastIndexOf(c,n);
s.lastIndexOf(t);
```
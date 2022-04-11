# Chapter 3 方法与参数

## 3.1 方法（函数）

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

在这个熟悉的 `HelloWorld`程序中，第一行定义了**类**，第二行则定义了**方法** `main`.

方法包含了若干行代码，它能够让代码的编写能够很方便地调用这些代码。

`main`是主方法，程序必须有主方法。运行程序时，执行的就是主方法内容。

### 3.1.1 方法的调用

对于上面的代码，我们也可以这样达到相同的效果。

```java
public static void method0() {
    System.out.println("Hello World");
}
public static void main(String[] args) {
    method0();
    method0();
}
```

以上代码中，我们定义了方法 `method0`, 该方法的作用是输出 `"Hello World"`. 然后，我们在 `main`函数中调用了两次该方法，输出结果为：

```java
Hello World
Hello World
```

### 3.1.2 返回值

上方 `HelloWorld`代码中，我们用 `void`**修饰符**修饰了 `main`函数。`void`指的是函数**没有返回值**。我们也可以用 `boolean, int, double, String`等修饰符来修饰函数。当函数函数有返回值时，函数内必须使用 **带值的** `return`. `return`能够**停止**函数的执行，并返回一个值。例如：

```java
public static int max(int a, int b) {
    int ret;
    if (a > b) {
        ret = a;
    } else {
        ret = b;
    }
    return ret;
}

public static void main(String[] args) {
    int a = 5;
    int b = 6;
    System.out.println(max(a,b));
}
```

以上函数运行的结果为：

```java
6
```

## 3.2 参数

在刚刚的例子中，我们可以看到，在调用方法 `method0`中，我们的代码是 `method0();` 也就是说，方法是可以拥有参数的，只不过刚刚的方法我们不需要参数的引入，只写了一个空的括号 `()`.

### 3.2.1 参数的传递

让我们看以下代码：

```java
public static void swap(int a, int b) {
    int t = a;
    t = a;
    a = b;
    b = t;
}

public static void main(String[] args) {
    int a = 5;
    int b = 6;
    swap(a, b);
    System.out.println("a = " + a + " b = " + b);
}
```

我们定义了一个方法 `swap()`, 我们想要用该方法交换 `a`和 `b`的值。但这样的代码能交换 `a`和 `b`的值吗？

代码运行结果如下：

```java
a = 5 b = 6
```

显然，并没有交换 `a`和 `b`的值。这是为什么呢？

这是因为，函数的参数在传递的过程中，传过去的只是**值**。换句话说，每个函数都有自己的**变量空间**，参数也位于这个**独立的**空间中，和其他函数没有关系。

另外，函数的参数也是需要指定数据类型的。与前文中提到的数据类型转换一样，期望数据类型比调用函数时给的值类型宽的时候，会自动转换。反之则需要写强制类型转换，例如：`(int)5.0`.

### 3.2.2 本地变量

函数的运行产生了一个独立的变量空间，在这个空间中的变量，是函数的这次运行所独有的，称作本地变量。

参数和定义在函数内部的变量都是本地变量。

### 3.2.3 变量的生存期和作用域

生存期：什么时候这个变量出现了、消亡了。

作用域：在什么范围内可以访问这个变量。

显然，对于本地变量来说，每一对大括号 `{}`内，就是这些变量的生存期和作用域。

我们将一对大括号 `{}`围成的结构称为**块**。

### 3.2.4 方法重(zhòng)载(zài) Method Overloading

我们可以使用相同的方法名，通过重载的方式来处理不同的参数，例如：

```java
public static int sum(int num0, int num1) {
    return num0 + num1;
}

public static double sum(double num0, double num1) {
    return num0 + num1;
}

public static void main(String[] args) {
    System.out.println(sum(1, 2));
    System.out.println(sum(0.1, 0.2));
}
```

以上代码中，我们对 `sum()`方法重载了两种数据类型——`int`和 `double`. 使得该方法既可以对整数求和也可以对双精度浮点数求和。

运行结果为：

```java
3
0.30000000000000004
```

通过该方法我们求出了两个和。不过，我们注意到，`0.1 + 0.2 = 0.30000000000000004`. 这里涉及到十进制与二进制转化中除不尽的问题，具体这里不再展开。如果要规避该问题，可以使用 `BigDecimal`工具类。

```java
BigDecimal b1 = new BigDecimal("0.1");
BigDecimal b2 = new BigDecimal("0.2");
BigDecimal b3 = b1.add(b2);
```

# Chapter 4 面向对象与类、实例、包

## 4.1 面向对象

面向对象(Object-Oriented Programming)是一种设计思想，它以对象作为基本单位，对象包括自己的属性(Attributes)和方法(Methods). 面向对象具有三大基本特征

**封装、继承、多态**。

* 封装（Encapsulation）：对外部世界隐藏内部实现的细节。
* 继承（Inheritance）：继承使子类具有父类的属性和方法，而不用编写相同的代码。
* 多态（Polymorphism）：为不同的数据类型的实现提供统一的接口。

## 4.2 类和实例

要理解类，我们首先看**对象**的概念：

**对象**：**对象是一个自包含的实体，用一组可识别的特性和行为来标识。**

简单来说，万物皆可为对象，对象就是某一种“东西”。

那么，什么是**类**？**类就是具有相同的属性和功能的对象的抽象集合**。

简单来说，就是一类东西。

**实例**又是什么？**实例**其实很好理解，**实例**就是一个具体的对象，用 `new`关键词创建一个具体的对象，这一过程称为**实例化**。

我们通过一个例子来展示上文所述的**对象、类**和**实例化**。

```java
public class Employee {
    String name = "Alice";
    int salary = 30000;

    public int getSalary() {
        return salary;
    }

    public void quitJob() {
        System.out.println("Bye");
    }

    public static void main(String[] args) {
        Employee employee = new Employee();
        System.out.println(employee.getSalary());
        employee.quitJob();
    }
}
```

以上代码中，我们定义了 `Employee`类，并创建了对象 `employee`（实例化），它具有 `name`和 `salary`两个属性。也有 `getSalary`和 `quitJob`两个方法。然后在 `main`函数中调用了这两个方法。

以上代码输出结果为：

```java
30000
Bye
```

## 4.3 constructor和this

上文的 `Employee`类还可以这样去写：

```java
public class Employee {
    String name;

    public Employee() {
        name = "Alice";
    }

    public static void main(String[] args) {
        Employee employee = new Employee();
        System.out.println(employee.name);
    }
}
```

我们可以注意到，这里我们没有在 `class` 下方对 `name` 属性进行初始化，而是创建了一个 `Employee()` 构造函数。**构造函数**用于初始化实例。每次使用 `new` 初始化实例时，它都会被调用。构造函数是不能有返回值的，并且函数名必须和类名一致。

还可以这样写：

```java
public class Employee {
    String name;

    public Employee(String name) {
        this.name = name;
    }

    public static void main(String[] args) {
        Employee employee = new Employee("Alice");
        System.out.println(employee.name);
    }
}
```

这里我们使用了 `this`, 并且为构造函数引入了参数 `String name`, 在 `new` 创建 `employee` 时也为参数赋值了。

`this`指向的是创建的实例 `employee` 本身。

## 4.4 包

包，package. 我们在前文的学习中一直都省略了包的存在。实际上，**包**是存在于**类**之上的一层结构。也就是说，例如上文的 `Employee`类应该是这样的：

```java
package test;
public class Employee {
	//code block to be executed
}
```

一个类的完整名字是package_name.class_name.

为什么要用包呢？这是因为，我们需要在对**命名空间**作出区分。每一个包都定义了一个新的**命名空间**，这样我们可以更好地管理.java文件们了。

应该很容易注意到，我们在之前的代码中修饰 `class`往往都用的 `public`. 它能够使该类在同一个包中都能被调用，换句话说，就是在**包作用域内**它的属性和方法都能被访问。

关于对 `class`的修饰见下节。

## 4.5 属性和方法的修饰符的

我们应该已经见过了 `public, static`等修饰符。实际上，Java拥有2种修饰符，分别为**访问控制修饰符**和非**访问控制修饰符**。

### 4.5.1 访问控制修饰符

对于类的成员而言，其能否被其他类所访问，取决于该成员的修饰词；而对于一个类而言，其能否被其他类所访问，也取决于该类的修饰词。

访问控制修饰符包括以下4个： `public, protected, default, private`.

#### 默认访问修饰符 不使用任何关键字

使用默认访问修饰符声明的变量和方法，对同一个**包**内的**类**是可见的。接口里的变量都隐式声明为 `public static final`,而接口里的方法默认情况下访问权限为 `public`.

#### 私有访问修饰符private

私有访问修饰符是**最严格**的访问级别，所以被声明为 `private` 的**方法、变量和构造方法**只能被**所属类**访问，并且类和接口**不能**声明为  `private`.

声明为私有访问类型的变量只能通过类中公共的 `getter` 方法被外部类访问。

`private` 访问修饰符的使用主要用来隐藏类的实现细节和保护类的数据。

#### 公有访问修饰符public

被声明为 `public` 的类、方法、构造方法和接口能够被**任何其他类**访问。

如果几个相互访问的 `public` 类分布在不同的包中，则需要  `import` 相应 `public` 类所在的**包**。由于类的继承性，类所有的公有方法和变量都能被其子类继承。

#### 受保护的访问修饰符protected

* 基类的 `protected` 成员是包内可见的，并且对子类可见；
* 若子类与基类不在同一包中，那么在子类中，子类实例可以访问其从基类继承而来的 `protected` 方法，而不能访问基类实例的 `protected` 方法。

### 4.5.2 非访问控制修饰符

非访问修饰符这里我们提2个：`static, final`.

#### static

`static` 用于修饰**方法**和**类变量**。

* **静态变量：**
  static 关键字用来声明独立于对象的静态变量，无论一个类实例化多少对象，它的静态变量只有一份拷贝。 静态变量也被称为类变量。局部变量不能被声明为 static 变量。
* **静态方法：**
  static 关键字用来声明独立于对象的静态方法。静态方法不能使用类的非静态变量。静态方法从参数列表得到数据，然后计算这些数据。

#### final

`final` 用于修饰**类**、**方法**和**变量**。

`final` 修饰的类不能够被继承，修饰的方法不能被继承类重新定义，修饰的变量为常量，是不可修改的。`final` 修饰符通常和 `static` 修饰符一起使用来创建类常量。

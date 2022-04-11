# Chapter 5 封装、继承、多态、抽象、接口

## 5.1 封装 Encapsulation

封装是一种控制用户对数据操作的方法。我们一般会将数据的访问控制修饰符改为 `private` , 然后通过  `get` 和 `set` 方法提供操作数据的接口。

例如：

```java
public class Game {
    private int score;
    public int getScore() {   
        return score;
    }
    public void setScore(int score) {
        if(score < 0 || score > 100) {
            System.out.println("Error");
            return;
        }
        this.score = score;
    }
}
```

在以上例子中，我们的 `Game` 类中有一个  `score` 变量，并为它设定了一组 `get` 和 `set` 方法。通过开放的这组方法来控制用户对 `score` 变量的读写行为。

## 5.2 继承 Inheritance

继承是创建一个与已有的类相似的类的操作。已有的类叫做**父类**或**基类**，派生出来的类叫做**子类**。子类会继承父类的数据和方法，并且可以修改原来的方法和添加新的方法。

```java
public class Animal {
    protected String name;
    public Animal(String name) {
        this.name = name;
    }
    public void greet() {
        System.out.println("Hello, I am " + this.name);
    }
}
```

我们定义了一个 `Animal` 类，它有 `name` 这个属性，并设定了一些方法。

这时，我们想创建一个 `Dog` 类，它和 `Animal` 相似，因此我们创建一个子类 `Dog` 继承父类 `Animal`.

```java
public class Dog extends Animal {
    public Dog(String name) {
        super(name);
    }
    public void greet() {
        System.out.println("WangWang..., I am " + this.name);
    }
    public void run() {
        System.out.println("I am running!");
    }
}
```

表示继承关系，应当使用语句：

```java
class 子类 extends 父类 {}
```

在子类 `Dog` 中，我们添加了一个新的方法：`run`. 并**重写(Override)**了方法 `greet`. `Dog` 继承了 `Animal` 的属性和方法。不过需要注意的是，以 `public` 和 `protected` 修饰的属性和方法才能被子类访问。这里在子类 `Dog` 里我们使用了 `super()` 方法，意思就是调用父类的 `Animal(String name)` 方法。

值得注意的是，在继承中，子类和父类的构造函数存在以下4个需要注意的点：

* 创建类时指定了有参数构造函数后，系统默认不会创建无参数构造函数，需要自己手动创建。
* 创建子类的对象实例时，默认会先调用父类的无参数的构造函数（默认构造函数）。
* 若父类未定义无参数构造函数，则在编译阶段报错。
* 若子类指定了父类的有参构造函数，则可以通过编译和运行。

## 5.3 多态 Polymorphism

多态指的是对不同类型的参数进行相同的操作，根据对象（或类）类型的不同而表现出不同的行为。多态往往是为了能够为不同的数据实现提供统一的接口。例如，我们再创建一个 `Animal` 的子类 `Cat`.

```java
public class Cat extends Animal {
    public Cat(String name) { 
        super(name);
    }
    public void greet() { 
        System.out.println("MiaoMiao..., I am " + this.name);
    }
}
```

容易看出，`Animal` 的两个子类 `Dog` 和 `Cat` 拥有不同的 `greet()` 方法。

我们在不同实例中调用不同的 `greet` 方法。

```java
public class Main { 
    public static void main(String[] args) {
        Animal cat = new Cat("cat");
        cat.greet(); // MiaoMiao..., I am cat
        Animal dog = new Dog("dog");
        dog.greet(); // WangWang..., I am dog
    }
}
```

运行结果为：

```java
MiaoMiao..., I am cat
WangWang..., I am dog
```

## 5.4 抽象 Abstraction

抽象 `Abstract` 是一种修饰**类**和**方法**的非访问修饰符。用它修饰的类**不能被实例化**，只能被**继承**。用它修饰的方法**只能**存在于**抽象类**中。当抽象类被继承时，子类**必须**调用抽象类中的抽象方法。当然，抽象类中除了有抽象方法，也可以存在普通方法，这些方法是可以不被子类调用的。

例如：

```java
public abstract class Person { 
    public abstract void greet();
    public void sleep() {
        System.out.println("Zzz");
    }
}
```

这里我们尝试对该类实例化，使用以下代码：

```java
Person person = new Person();
```

这样会出现以下错误提示：

```java
Cannot instantiate the type Person
```

我们这里创建一个子类 `Teenager` 来继承 `Person`. 代码如下：

```java
public class Teenager extends Person {
    public void greet() {
        System.out.println("I am a teenager.");
    }
}
```

然后这里我们实例化 `Teenager`.

```java
public static void main(String args[]) {
    Teenager teenager = new Teenager();
    teenager.greet();
    teenager.sleep();
}
```

我们在子类 `Teenager` 中定义了方法 `greet`, 而没有定义方法 `sleep`. 在抽象类 `Person` 中，`greet` 方法是抽象方法，而 `sleep`不是。我们如果尝试不定义，则会提示以下错误：

```Java
The type Teenager must implement the inherited abstract method Person.greet()
```

值得注意的是，`abstract` 也是和 `final`, `static` 矛盾的。

另外，抽象方法是不能拥有函数体的，如果我们为抽象函数写上函数体，则会提示以下错误：

```java
Abstract methods do not specify a body
```

## 5.5 接口 Interface

接口也是一种抽象的策略。接口与上文的 `abstract` 比较类似，不过不同的就是 `interface` 只用来修饰**类**。用 `interface` 修饰的类可以认为是一个完全的**抽象类**。它是一个抽象方法的集合，不包含任何的逻辑代码，更像是为具体的类中要实现的方法构建了一个框架。不过，接口是**隐式抽象**的，接口和方法**都不需要**再使用 `abstract` 来修饰。

接口的声明语法格式如下：

```java
[可见度] interface 接口名称 [extends 其他的接口名] {
        // 声明变量
        // 抽象方法
}
```

例如，我们定义一个 `Student` 接口：

```java
interface Student {
    public void goToSchool();
}
```

实现接口 `implements`:

```java
public class Person implements Student { 
    public void goToSchool() {
        System.out.println("I'm going to school.");
    }
}
```

接口中的方法是需要**全部实现**的，否则会报错。同时，一个类是可以实现多个方法的，例如：

```java
public interface Employee { 
    public void goToWork();
}
```

```java
public class Person implements Student, Employee { 
    public void goToSchool() {
        System.out.println("I'm going to school");
    }
    public void goToWork() {
        System.out.println("I'm going to work.");
    }
}
```

这样，我们可以在 `Person` 类中调用这两个接口中的方法了。

```java
public class main {
    public static void main(String[] args) {  
        Person person = new Person(); 
        person.goToSchool();
        person.goToWork();
    }
}
```

# Chapter 2 条件判断和循环

## 2.1 条件判断

### 2.1.2 if

```java
int score = 60;
String level;
if (score >= 90) {
    level = "A";
} else if (score >= 80) {
    level = "B";
} else if (score >= 60) {
    level = "C";
} else {
    level = "D";
}
System.out.println(level);
```

以上代码运行结果为

```java
C
```

以上代码展示了成绩分等的分段函数的 `if, else if, else`实现。

实际上，`if`的判断语句返回的是布尔值。因此，我们也可以使用布尔值作为判断条件，例如：

```java
boolean win = true;
if (win) {
    System.out.println("Congratulations!");
}
```

### 2.1.3 switch case

```java
char level = 'D';
switch (level) {
    case 'A':
    System.out.println("很好!");
    break;
    case 'B':
    case 'C':
    System.out.println("加油！");
    break;
    case 'D':
    System.out.println("努力！");
    default:
    System.out.println("好好学习，天天向上");
```

以上代码运行结果为：

```java
努力！
好好学习，天天向上
```

`switch()`括号内的变量类型可以是：`byte, short, int, char, String`. `case`称为**标签**，标签后必须跟**常量**。

当 `switch case`执行时，会将 `switch`的表达式的值与各 `case`依次比较。当相等时，执行 `case`的语句，`case`的语句可以为空。同时，如果没有 `break`, 会继续执行下一个 `case`. 如果没有一个 `case`相匹配，那么则执行 `default`. 如果没有 `default`, 那么 `switch`就执行结束。

## 2.2 循环

### 2.2.1 for循环

`for`循环是一种非常常用的循环，通常适用于知道确定的循环次数时使用。

例如，我们通常使用 `for`循环来遍历数组。

```java
int[] array = { 1, 2, 3 };
for (int i = 0; i < array.length; i++) {
    System.out.print(array[i] + "\t");
}
```

以上代码运行结果为：

```java
1       2       3
```

当然，也可以这样：

```java
String[] students = { "Alice", "Bob" };
for (String student : students) {
    System.out.print(student + "\t");
```

以上代码运行结果为：

```java
Alice   Bob
```

我们也可以通过 `for(type variableName: arrayName)`来遍历数组。其中，`variableName`是可以任意取的。

### 2.2.2 while循环

`while`循环分为两种，一种是 `while`，另一种是 `do...while`.

这是 `while`.

```java
while(condition) {
    // code block to be executed
}
```

这是 `do...while`.

```java
do {
    // code block to be executed
} while (condition);
```

这两种循环很像，但是 `do...while`在循环执行结束时才判断条件，也就是说，循环至少会执行一次。根据合适的情境选择即可。

### 2.2.3 break与continue

`break`和 `continue`是循环控制中常用的两种方法。`break`表示跳出当前循环，`continue`表示跳出循环这一轮剩下的语句并进入下一轮。

在前文的 `switch...case`中已经见过break. 值得注意的是，`break`只能跳出当前循环。若要跳出多层循环，必须使用多个 `break`, 或者使用 `goto`.

我们举一个例子来说明 `continue`的用法。

```Java
int num[] = {1,2,3};
int sum = 0;
for (int i = 0; i < num.length; i++) {
    if (num[i]>=2) continue;
    sum += num[i];
}
System.out.println(sum);
```

运行结果为：

```java
1
```

上面的代码我们在 `{1，2，3}`这个数组中计算了小于2的数的和。在遍历中通过 `continue`跳过了对不满足条件的元素。

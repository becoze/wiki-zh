# 📌 多态 Polymorphic (1. 基本)

<aside>
💡 多态：**方法或对象**具有多种形态，多态是建立在封装和继承基础之上的。可以更加提高代码复用性，扩展性 和 维护性。

</aside>

多态有：**1. 方法的多态**，和 2. **对象的多态**

# 没有多态 vs 使用多态

[📃 [练习]不用多态的劣势](https://www.notion.so/c6023f2062e64e23aa24a2ac9379ecad?pvs=21)

[📃 [练习]多态优势](https://www.notion.so/025aa1314a974143b8b0a1ae078f2ef5?pvs=21)

## 方法的多态

<aside>
💡 方法重载，覆盖是一种多态的体现

</aside>

### 重载

**方法重载**的多态**：**传入的参数的不同 → 调用不同的方法。

[重载 Overload](https://www.notion.so/Overload-632a89dd66244e288cb451874763a0ed?pvs=21)

```java
// 方法重载体现的多态
A test = new A();
test.printSum(1, 2);     // 传入两个参数
test.printSum(1, 2, 3);  // 传入三个参数
```

### 重写

**方法重写**的多态：使用不同的类型（有继承关系）调用方法 → 调用不同的方法。

[方法覆盖/重写 Override](https://www.notion.so/Override-3500a87c20c240ef932255a9f4918241?pvs=21)

```java
// 方法覆盖体现的多态
A a = new A();
B b = new B();

a.printSum(10, 20);  // A 类的方法
b.printSum(10, 20);  // B 类的方法
```

```java
class A{
	public void printSum(int a, int b){
		System.out.println(a + b);
	}
	public void printSum(int a, int b, int c){
		System.out.println(a + b + c);
	}
}
```

```java
class B extends A {
	public void printSum(int a, int b){
		System.out.println(a + b);
	}
}
```

# Polymorphic - 对象的多态

<aside>
💡 多态 polymorphic 通常指**对象的多态。**多态的前提是：**两个对象（类）存在继承关系**。

</aside>

## 编译时类型 和 运行时类型

|  | 编译时类型 | 运行时类型 |
| --- | --- | --- |
|  | Compile-time Type | Runtime Type |
| 别称 | 静态类型 | 动态类型 |
| 解释 | 指变量、表达式或方法参数声明时所用的类型 | 指对象在内存中所真正引用的类型 |
| 定义位置 | 定义时，= 号的左边 | 定义时，= 号的右边 |
| 阶段 | 在编译阶段确定的 | 在程序实际执行时确定的 |
| 作用 | 编译时类型决定了编译器对代码进行类型检查和语法分析时所采用的类型 | 使变量可以在运行时引用不同的子类对象 |

## 对象的多态

<aside>
💡 **父类**的引用指向**自己或子类**的对象。

1. 一个对象的编译类型和运行类型**可以不一致。**
2. 编译类型在定义对象时，就确定了，**不能改变**。
3. 运行类型是**可以变化**的。
</aside>

```java
// 父类的引用指向自己的对象。
Animal animalx = new Animal(); // 1. 可以一致。 animal 编译类型是 Animal，运行类型 Animal。

// 父类的引用指向子类的对象。
Animal animal = new Dog();     // 1. 可以不一致。animal 编译类型是 Animal，运行类型 Dog。
animal = new Cat();            // 3. 运行类型可以变化。变化成 Cat。
															 // 2. 编译类型不可以改变
```

```java
class Animal {
    void makeSound() { System.out.println("Animal makes a sound"); }
}

class Dog extends Animal {
    void makeSound() { System.out.println("Dog barks"); }
}

class Cat extends Animal {
    void makeSound() { System.out.println("Cat meows"); }
}

public class Main {
    public static void main(String[] args) {
        Animal animal1 = new Dog();
        Animal animal2 = new Cat();
        
        animal1.makeSound();  // 输出是 "Dog barks"
        animal2.makeSound();  // 输出是 "Cat meows"

				animal1 = new Animal();  
				animal1.makeSound();  // 此时输出是 "Animal makes a sound"
    }
}
```
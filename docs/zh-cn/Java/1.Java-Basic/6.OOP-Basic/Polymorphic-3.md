# 📌 多态 Polymorphic (3. 调用属性&方法, instanceof)

# 属性没有重写

<aside>
💡 属性的值直接看**编译类型**的类。属性没有重写之说。
方法的值看**运行类型**的类。

</aside>

## 属性 & 方法

```java
public class Main{
	public static void main(String[] args){
		Animal test1 = new Cat();          // 向上转型
		System.out.println(test1.count);   // 属性 输出:10, **编译类型**是 Animal
		test1.print();    // 方法 输出:20, **运行类型**是Cat,调用Cat的print

		Cat test2 = new Cat();   
		System.out.println(test2.count);   // 属性 输出: 20, **编译类型**是 Cat
		test2.print();    // 方法 输出:20, **运行类型**是Cat,调用Cat的print
	}
}

class Animal{
	int count = 10;
	public void print(){ System.out.println(this.count) }
}
class Cat extends Animal{
	int count = 20; 
	public void print(){ System.out.println(this.count) }
}
```

# instanceof 比较操作符

<aside>
💡 instanceof 比较操作符。返回 True / False。`name instanceof XXX;`
用于判断**对象**的**运行类型**是否为XXX类型，或XXX类型的子类型。

</aside>

```java
public class Main{
	public static void main(String[] args){
		Cat test = new Cat();
		// test1是Cat/Animal类型，或是Cat/Animal类型的子类型吗？
		System.out.println(test instanceof Cat);    // true，test1的**运行类型**是Cat类型
		System.out.println(test instanceof Animal); // true，test1的**运行类型**是Animal的子类型

		Animal test2 = new Cat();
		// test2是Cat/Animal类型，或是Cat/Animal类型的子类型吗？
		System.out.println(test instanceof Cat);    // true，test2的**运行类型**是Cat类型
		System.out.println(test instanceof Animal); // true，test2的**运行类型**是Animal的子类型

		Object obj = new Object();
		System.out.println(obj instanceof Animal); // false，obj不是Animal类或它的子类

		String str = "aaa";
		System.out.println(str instanceof Object); // true，str是Object下的类型。
		System.out.println(str instanceof Animal); // Error，str是字符串，无法比较
	}
}

class Animal{ ... }
class Cat extends Animal{ ... }
```
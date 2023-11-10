# 📌 多态 Polymorphic (2. 向上/下转型)

# 向上转型

**向上转型：**父类的引用指向了子类的对象。`父类引用 name = new 子类类型();`

1. 在**编译阶段**，只能调用父类的所有成员，但不能调用子类的特有的成员。因为在**编译阶段(javac)**，能调用那些成员是由**编译类型**`Animal`决定的。
    1. 也包括父类的父类（父类的父类本质直接父类继承了**所有**成员*）
2. 在**运行阶段，**最终的运行结果要看子类的具体实现。因为在**运行阶段(java)，**是先从**运行类型（本类`new Animal()` 或子类 `new Cat()`）**开始查找。和继承的 super 成员调用一致。
   
    > [📌 继承 Extends (4. super() 和 super. 的使用）](https://www.notion.so/Extends-4-super-super-1ed7d37062db4397a2de097ec0b84974?pvs=21) - 两种调用成员的顺序
    > 
    > 1. 首先看**运行类型**是否有该属性，如果有这个属性，**并且可以访问**，则返回信息；**否则直接报错**。
    > 2. 如果**运行类型**没有这个属性，就向上查找父类有没有这个属性，如果父类有该属性，**并且可以访问**，则返回信息；**否则直接报错**。
    > 3. 如果父类没有就按照(2)的规则，继续找上级父类，直到Object。
3. 同样要遵守访问权限。

成员：方法，属性，构造器，以及其初始化等 

```java
编译类型 name = new 运行类型();
向上转型：父类类型 name = new 子类类型();
Object obj = new Cat();    // OK 1. Object是Cat的父类
Animal animal = new Cat(); // OK 1. 编译类型-Animal(), 运行类型-Cat()
animal.catchMouse();   // Error 1. Animal没有catchMouse
animal.eat();          // OK    2. 输出的是Cat的"Eat Fish",而不是Animal的eat
animal.sleep();        // Error 3. Animal的sleep是私有方法。

class Animal {
	String name;
	public void eat(){};   // overridered
	private void sleep();
}
class Cat extends Animal {
	public void eat(){ sout("Eat Fish") };   // override
	public void catchMouse(){};
}
```

# 向下转型

**向下转型：**把父类的引用强行转化成子类的类型。当向下转型后，就可以**调用子类类型的成员**。

1. 只能强转父类的**引用**`anmial`，不能强转父类的**实例化对象**`new xxx()`**。**
2. 要求**父类的引用**`animal`必须指向是当前目标类型的对象。
   
    `Animal animal = new Cat();` animal = Cat
    
    1. `Cat cat = (Cat) animal`，animal → Cat。转换OK ✅
    2. `Dog dog = (Dog) animal`，animal → Dog。转换不能 ❌
    3. `~~Dog dog = (Cat) animal`，？？？。转换不能~~ 

```java
编译类型 name = new 运行类型();
向上转型：子类类型 name = (子类类型) 父类**引用**;
Animal animal = new Cat();  // OK 1. 编译类型-Animal(), 运行类型-Cat()
Cat cat = (Cat) animal;     // OK 1. 编译类型-Cat(), 运行类型-Cat()
cat.catchMouse();           // OK 可以调用子类类型的成员

class Animal {
	String name;
	public void eat(){};
	private void sleep();
}
class Cat extends Animal {
	public void eat(){ sout("Eat Fish") };
	public void catchMouse(){};
}
```
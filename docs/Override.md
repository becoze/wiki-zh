# Override





aaaaaaaaaaaa







# **方法名、返回类型（或同类）、参数完全一样**

<aside>
💡 子类有一个方法，和父类的某个**方法名、返回类型（或同类）*、参数完全一样**。那么我们就说子类的这个方法覆盖了父类的方法。

▪️子类方法的返回类型和父类方法**返回类型一样，或者是父类返回类型的子类**。比如父类返回类型是Object，子类方法返回类型是String。

</aside>

✅ 同方法名

✅ 同返回类型（String是Object的子类）

✅ 同形参

```java
class A {
	public Object method(String a){ }
}

class B extends A{
	public String method(String b){ }
}
```

✅ 同方法名

✅ **同返回类型（BBB是AAA的子类）**

✅ 同形参

```java
class AAA {
	public AAA method(){ } // 自己的类型
}

class BBB extends AAA{
	public AAA method(){ } // 父类的类型
}

class Text extends BBB{
	public BBB method(){ } // 父类的类型
	// or
	public AAA method(){ } // 父类的类型
}
```

# 子类方法不能缩小父类方法的访问权限

[访问修饰符 Access modifier](https://www.notion.so/Access-modifier-905d735a658f4d70a070cd89b26e2643?pvs=21)

```java
public > protected > [default] > private

🆙 可以扩大： private → public
➖ 可以不变： [default] → [default]
🚫 不可以缩小：public → private
```

❌ 缩小了父类方法的访问权限

```java
class A {
	public void method(String a){ }
}

class B extends A{
	public void method(String a){ }
	// or 
	void method(String a){ }
}
```

✅ 没有缩小（扩大了）父类方法的访问权限

```java
class A {
	private void method(String a){ }
}

class B extends A{
	// Error
	public void method(String a){ }
}
```

# 方法重写 vs 方法重载

| 名称 Name | 发生范围 | 方法名 | 形参列表 | 返回类型 | 修饰符 |
| --- | --- | --- | --- | --- | --- |
| 重载 (Overload) | 当前类 | 要求相同 | 要求不同 | 无要求 | 无要求 |
| 重写 (Override) | 之间有继承关系的所有类 | 要求相同 | 要求相同 | 子类的返回类型要求和父类相同，或是父类返回类型的子类。 | 子类的修饰符不能缩小父类的访问范围。 |
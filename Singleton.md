一、单例模式

### 1. 定义：

> 一个类只提供一个实例，并提供全局访问点。

### 2. 单例模式的几种实现方式

- 饿汉式（基于classloder机制避免了多线程的同步问题）

```java
public class SingletnHungry {
	private static SingletnHungry instance = new SingletnHungry()
	private SingletnHungry(){}
	public static SingletnHungry getSingletnHungry() {
		return instance
	}
}
```

>  ***Note:*** 在使用这种方式使会有一种潜在的问题：即无法避免在序列化和反序列化时，会绕过`private`构造方法，从而创建出多个实例。

- 懒汉式（即延迟加载，在第一次调用时才初始化实例）

```java
public class SingletnHungry {
	private static SingletnHungry instance = null
	private SingletnHungry(){}
	public static SingletnHungry getSingletnHungry() {
		if(instance == null) {
			instance = new SingletnHungry()
		}
		return instance
	}
}
```

> 这种方式存在多线程加载时会出现错误，需要给整个方法加锁

```java
	public synchronized static SingletnHungry getSingletnHungry() {
		if(instance == null) {
			instance = new SingletnHungry()
		}
		return instance
	}
```

> 这种写法虽然能解决多线程下避免资源竞争时出错的问题，但是这种写法会严重影响并发性能

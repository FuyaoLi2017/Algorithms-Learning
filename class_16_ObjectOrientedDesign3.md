# OOD3
Use case -> Classes and their relationships -> States and behaviors -> code

# Simple Design Patterns
目标：
1. 了解常见的设计模式， 深刻理解他们的motivation
2. Singleton写一个

### Example
加一个必填的constructor, 后面的setter和getter

limitations:
- What if we do not want to expose setters for some data fields?
- 需要多个调用才能完成object creation, 语义上无法确定User object什么时候构建完成

##使用builder pattern:
- Java很常用
- C++很不常用
    - C++ const很明确的可以确定，不存在需要解决“ What if we do not want to expose setters for some data fields?”，所以收益相对较小

## 使用factory pattern:加一层抽象
抽离出对象创建的逻辑
1. separate instance/
2. More clean especially when we have complicated instance creation logic
3. Easier to extend the instance creation logic (extend to ): 实现对象回收等，提升性能
4. Provide chances to have different object allocation strategies(e.g. what if we want to reuse shape objects)

每个类只做一件事情，单一责任原则，加上一层抽象。extends出来，有些地方叫 **factory method**

## Abstract Factory
The abstract factory pattern provides a way to encapsulate a group of individuals factories that have a common theme without specifying their concrete classes.

## Singleton Pattern
Ensure a class has only one instance, and provide a global point of access to it. Why?
- Only one instance in the world: focused phone screen, database connection, data buffer, etc.
- eager initialization(饿汉模式)
```Java
public class SingletonExample {
    private static final SingletonExample INSTANCE = new SingletonExample();

    private SingletonExample() {}

    public static SingletonExample getInstance() {
        return INSTANCE;
    }
}

```

1. has an INSTANCE
2. only one, no one else can create -- private control
3. global accessible -- public static getter

- lazy initialization(懒汉模式) (cost of construction is very high, may not be used after initialization)
1. init cost expensive
2. rarely used, may not access
```java
public class SingletonExample {
    private static final SingletonExample INSTANCE = null;

    private SingletonExample() {}

    public static SingletonExample getInstance() {
        if (INSTANCE == null) {
            INSTANCE = new SingletonExample();
        }
        return INSTANCE;
    }
}

```

- concurrency并发问题下面的singleton

- Controversy:
    - Strong limitation: you cannot have two instances
    - Treated as a "global variable", hides dependencies (who used it?) and holds global states.
    - Hard to build unit test(hard to fake it, test results may be order-dependent)
- Program to interface, not implementation, SINGLETON 不能实现这一点

- Disadvantages of lazy initialization
    - Underterministic runtime behavior, critical in user-facing serving system

NEO 老师
cpp@laioffer.com
3 advices to answering design questions:
1. 文无第一，武无第二:
- system design没有最好，只有合适。
- 算法的复杂度，总是有最好的结果。
2. 尽信书不如无书，过程比结果更重要:
- 变通设计模式，选择最合适的工具使用
3. 冰冻三尺非一日之寒:
- 人月神话
- 长期积累学习

### OOD 1,2: Object Oriented Programming, Basic steps in OOD
### OOD 3: Design patterns
### OOD 4: More advanced examples

# Why learning OOD?
1. Practical problems -> Model -> Code
2. Better understanding of OOP
3. How to write good code

OOD 1
1) Key concepts of Objected Oriented Programming/Design

Reading Material:
1. Effective Java(Effective C++)
2. Java source code(eg. ArrayList, LinkedList, HashMap, PriorityQueue...)

What if I'm new to Java/C++?
1. Use a text book(Head Frist Java, Thinking in Java, Thinking in C++, C++ Primer)

What's is good code, what is a good design?
1. Complete functionality
2. Easy to use (by others)
- Clear, elegant, easy to understand, no ambiguity
- Prevent users from making mistakes

3. Easy to evolve (more important than revolution)
- Motivation of Object Oriented Programming
    - Structured programming: code + data
        - if a list of data is apprearing for many times and they always use a set of function. ArrayList: array + operations on Array
    - What if we want to use limited interface(API)?
    examples: List
        - APIs, application programming interface (private attributes, private methods): how to store elements in the list, how to track its size.
    - Using inheritance to use the existing codes and realize aiming at different examples

## Basic concepts
#### 2.1 Class and Object
- Class: a blueprint for a datatype, scheme
- Object: a specific realization of any class, instance

#### 2.2 Data Encapsulation: data abstraction and acess labels
1) Providing only essential information to the outside world and hiding their background details
2) Separate interface and implementation
3) Access Modifier: public, private, protected, default

| Access | public(API) | protected | private |
| ------ | ------ | ------ | ------ |
| Same Class | yes | yes | yes |
| Derived classes |  yes | yes | no |
| outside classes |  yes | no | no |

Application Programming Interface

Java access level


| Modifier | class | package | Subclass | World |
| ------ | ------ | ------ | ------ | ------ |
| public | yes | yes | yes | yes |
| protected |  yes | yes | yes | no |
| no Modifier |  yes | yes | no | no |
| private |  yes | no | no | no |

No nesting relationship in Java package! 都是独立的个体，没有嵌套关系, package都是完全独立的

### How to select appropriate labels? (feature owned by OOP languages)
给尽量低的权限
1. API: public
2. Internal implementation: private
3. class inheritance: do we need to use protected for methods/attributes
- a. Protected methods: sometimes useful when when we want to override an implementation in subclasses
- b. Protected attributes: be careful, try to use private first (protected getter() / setter()) eg. protected getter only(read only)
4. "default": in java (package-private): declare a class as public only when we define public API in it, otherwise package-private is good enough.

## Inheritance, Interface, Abstract class
### 2.3.1 Inheritance, Base class, Derived class
Employee -> Manager/Programmer

List -> ArrayList/LinkedList

体现不同class的共性！
#### In java, for base class, Inteface v.s. Abstract class v.s. Concrete class?
1. An abstract class provides a common base class implementation to derived classes.
2. Interface helps you (or enforces you) to focus on the API siguature definition.
interface Collection: add(E), size(), contains(Object)...
3. Mutiple inheritance: implement multiple interfaces
4. The relationship between the interface itself and the class implement implementing the interface is not necessarily strong.


- 父类： 表示属性
- 接口：体现能做什么，capable of doing

## Polymorphism and overriding

a call to a member function will cause a different function to be executed depending on the type of object that invokes the function.

从需求入手

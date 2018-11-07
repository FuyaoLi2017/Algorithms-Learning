Nov 4th Class Class, Objects and references
> Zoom use touch bar to switch to earphone， setting

### 1. Static Keyword
- 属于类型本身，独立于类型的任何一个具体的object
- 所有对象共享这个static
- 在load class时候生成
- 非静态的对象用object reference调用
- 调用静态对象用类名调用(用reference会产生warning)
- static method 直接调用的必须是static method.

### 2. Final Keyword
#### once assigned, cannot be changed
- Final class: a class cannot be derived
- Final method: a method cannot be overriden
- Final field: a variable once assigned, cannot be assigned again

For final in use
- primitive type：the value cannot be changed
- reference: the address cannot change, the value assigned to it can change

### 3. Parameter Passing
method modifier
> - private: class itself visable
- public: all visiable
- protected: package and child class visiable
- default: package visable

#### Java is always pass by value
- primitive type: copy the value itself
- objects: copy the object reference
- dereference find the value on the value, and modify it
- 第一个例子，passing the value to x, a different object to the former x. modify it will not change the value of outside x.
```Java
int x = 5;
changeIntValue(x);
System.out.println(x);  // print 5

private static void changeIntValue(int x) {
  x = 10;  // this x is different from the former x
}
```


### 4. Primitive type
- byte
- boolean
- short
- char: 2 bytes
- int: 4 bytes
- float
- double
- long

连续存储；random access是O(1)

1. 默认：零假空：赋初始值特点
2. char是0

### 5. Array
int[][] array = new int[2][3];
2 layer structure, a reference contains 2 references for two 1-d array.

array倾向于是矩形，如果非矩形建议List<List<>>

#### Exception
- ArrayIndexOutOfBoundException;
数组越界

- NullPointerException;
数组取到的对象是null

- null & length => 0: the array's address don't exist & the length of array is 0

compile error
runtime error

### 6. Writing code in google doc
1. Font: courier new
2. Format: tools: preference, close the auto capitalization
3. Indetation: use tab, no space

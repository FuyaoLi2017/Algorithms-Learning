# 1 读java doc方法
### java.util等
所在的包

### 继承关系
- 实体类有写继承树的关系，java只能单继承。
- class可以implement多个interface: interface 本身没有implements

### method
- specified by: 是从其他位置继承过来的。

### constructor summary
- **new** 的时候会用到，实体类才会有。

- stack: thread safe
- stack继承自vector,也是废弃的方法

# 2. program against interface

##例子
### input parameter
- 写成 public void sort(List<Integer> array) {

}

### List<List<Integer>> list = new ArrayList<List<>>;  right!
尖括号里面的generic是不会new的

### List<List<Integer>> list = new ArrayList<ArrayList<>>; wrong!
尖括号里面的不能实例化

## 接口编程优势
- more flexible  
a function whose parameter is interface can take any object types that are implementations of the interface.

- more extensible  
in the future, if there is another implementation of the List interface, there is no need to modify the print function which can be directly used.

### subset的题目2种解法
```java
```

```java
```
#### RECURSION
**把大的问题分成同性质的小问题，用同样的方法解决小问题，用小问题的解构造问题的解**

- subproblem
- recursion rule
- base case

#### for this problem:
- subproblem: "ab"s all subsets ["", "a", "b", "ab"]
- recusion rule: ["", "a", "b", "ab"] ["c", "ac", "bc", "abc"]
- base: "" -> [""]

```java
```
- TC:也是O(2^n)

- 空string和null: 含义不同，要返回一个正确的结果

做题想思路的时候不能画recursion tree, 否则不容易抽象出问题的主干。

### debug， 注意corner case, empty string不一样

backtracking，回到原来的节点，样子还是原来的样子

### permutation
**“abc” -> all permutations**
- subproblem: "ab" -> ["ab", "ba"]
- recursion rule: ["ab", "ba"]
- base case: "" -> [""]
```java
```

### better view of recursion: 形式逻辑
务必大胆的假设recusion子问题的解是正确的

#### 类似于数学归纳法 induction
- subproblem: K的情况
- recusion rule: K + 1的情况
- base case: 0的情况

#### String是immutable的，string的toString()会new String.
#### 如果是容器，做backtracking必须是new出来。
是不是immutable的话是backtracking是不是需要new的条件。

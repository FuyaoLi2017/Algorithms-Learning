# Review
- Array
- linkedlist

# Queue & Stack
- Array, linkedlist是物理层面的数据结构
- Queue, Stack是逻辑层面的operation

## 1. Queue


## 2. Stack
### (1)How to sort numbers with three(or two) stacks



#### (i) three stacks
questions: all unique elements? 需要多维护一个counter
1. 维护一个global min
Stack1: unsorted numbers  
Stack2: buffer/scratch space  
Stack3: sorted numbers  

#### （2）two stacks
stack1 []  
stack3&2 [1 2 3 | 4]

int globalMin = 3, counter = 1
挡板以隐式的方式写出来。如果一样的话直接把相同的数字pop出来。

#### (3)three stack实现merge sort

#### (4) how to implement a queue using a stack or multiple stacks

amortized time complexity 平摊分析

### difference between amortized and average time complexity:
average: 多种情况下平均的时间复杂度
amorized: 在所有的情况都是这个时间复杂度，平均的是同一个情况不同阶段做平均

#### （5）How to implement a stack using two queues?

swap是交换的reference,并不是每个都要实现

#### （6）How could we implement a stack by using one queue, assuming we can get the size of the queue at any time?

需要记录stack长度

#### （7）implement min() function when using stack with time complexity O(1)

维护一个数组保存push进来的数字在此数字及其之前的最小值

stack1 [3, 1, 2
stack2 [3, 1, 1  // store min element so far in stack1

- follow up: How to optimize the space usage of stack2 assuming the elements are many duplicates

优化1：  
存一个pair数组，包含一个数字 * 个数

stack1 [1 1 1 1 1 2 2 2 1 1 0 0
stack2 [<value = 1, counter = 10>, <value = 0, count 2>...

优化2：
记录数字和它的起始位置也可，把优化2 counter改成position,这样不用更新counter这个位置

#### （8）How to use multiple stacks to implement a deque

##### 2 stacks
      stack1  stack2
           ]  [    
- addLeft: stack1.push()
- addRight； stack2.push()
- removeLeft: O(n) in worst case, **can't be amortized**, if removeLeft and removeRight repeatly case
    - Case1: if stack1 is not empty, stack1.pop()
    - if stack1 is empty, move all numbers from stack2 to stack1, stack1.pop()
- removeRight: O(n) in worst case
    - Case1: if stack2 is not empty, stack2.pop()
    - Case2: if stack2 is empty, move all numbers from stack1 to stack2, stack2.pop()

- 优化：**can be amortized**
加一个stack3, use this as a buffer, keep a size of the stack，banlance both the two stacks have half of the elements
    - stack1 -> half of it put into stack3
    - stack1 second half put in stack2
    - stack3 -> put back into stack1


# When to use Stack? Queue?
## 1. when to use stack?
### 从左到右linear scan一个array/string,如果要不断回头看左边最新的元素，需要用到stack
    - reverse polish notation 逆波兰表达式的计算
    >https://blog.csdn.net/QZC295919009/article/details/23799369
    >https://blog.csdn.net/linraise/article/details/20459751


算法：中缀表达式转换成后缀表达式
输入：中缀表达式串
输出：后缀表达式串
PROCESS BEGIN:

1.从左往右扫描中缀表达式串s，对于每一个操作数或操作符，执行以下操作;  
2.IF (扫描到的s[i]是操作数DATA)  
  将s[i]添加到输出串中;   
3.IF (扫描到的s[i]是开括号'(')  
  将s[i]压栈;  
4.WHILE (扫描到的s[i]是操作符OP)  
  IF (栈为空 或 栈顶为'(' 或 扫描到的操作符优先级比栈顶操作符高)  
  将s[i]压栈;  
  BREAK;  
  ELSE  
  出栈至输出串中  
5.IF (扫描到的s[i]是闭括号')')  
     栈中运算符逐个出栈并输出，直到遇到开括号'(';  
     开括号'('出栈并丢弃;  
6.返回第1.步  
7.WHILE (扫描结束而栈中还有操作符)  
  操作符出栈并加到输出串中  
PROCESS END  


### String的repeatedly deduplcation.(第8节课会详细讲解)

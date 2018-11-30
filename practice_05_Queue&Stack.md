# Stack and Queue Implementation

## Queue
- throw exception: 正常使用时候不会为空用这组API
    - Insert: add()
    - Remove: remove()
    - Examine: element()
- return special value(null): 正常使用时候可能为空用这组API
    - Insert: offer()
    - Remove: poll()
    - Examine: peek()

## Deque
- eager calculation：size()实现：每次更新内容 都重新算一下size
Stack<Integer> //Deprecated
- LinkedList Implementation
Deque<Integer> stack = new LinkedList<>(); // prefer  
- Array Implementation
Deque<Integer> stack = new ArrayDeque<>();

- push()
- pop()
- peek()

size()在implement时候返回类型是int, 其他可能是null的返回类型必须是wrapped class，必须是Integer等。

int -> Integer: boxing  
Integer -> int: inboxing

# Queue
不一定不需要使用double linked list, 可以保留2个方向的reference

peek()不能直接return head，因为不能返回reference，是返回值

### Array实现
用array实现queue,把array当成一个环,维护head和tail 2个指针

tail = (tail + 1) % array.length

#### 判断空/满
- 没有size的话可以让一个格子为空，该格子指向tail
    - empty: head == tail
    - full: (tail + 1) % len = length
- 有保存size
    - empty: size == 0
    - full: size == array.length


尝试实现的时候加一个java实现类，对比着分析测试样例。

Homework：写上课写的code.

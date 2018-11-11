# LinkedList

### 1. Structure of LinkedList
- LinkedList的下一个元素的位置由next指定，next这个field是下一个元素的address -> 内存中不是连续的

### 2. Key points
1. When you want to dereference a ListNode, make sure it is not a NULL NullPointer
i.e.  
对于用到的索引都必须要检查是否会涉及到dereference,每一个"."都保证是非null，才能安全进行dereference

```java
ListNode p = new ListNode(10);
p = null;

if (p != null && p.next != null) {
    p.next.value;
}

int[] a = {1,2,3}

if (x >= 0 && x < a.length)
a[n + 1 - i]
```
2. Never ever lose the control of the head pointer of the LinkedList
反转链表的过程中必须是向后转移链表的点  



### (1) interview question on linkedlist: how to reverse a linked list

Node1 -> Node2 -> Node3 -> Node4 ...-> NodeN -> NULL
                            next
         prev
                   head


reversed:   NULL <- Node1 <- Node2 <- ... <- NodeN

#### iterative method
```java
public ListNode reverse(ListNode head) {
    ListNode prev = null;
    // no need to implement the corner case, if the list is null,
    while (head != null) {
        // initiate a next pointer, points to the next value
        ListNode next = head.next;
        // change the point direction of the head
        // pointing the point after the node to before the point
        head.next = prev;
        // make head point to the prev point
        prev = head;
        // make the head point to the next position
        head = next;
    }
    return prev;
}
```

#### recursive method
// subproblem: the node2 to the last node is reversed
(1) next -> next = cur // subproblem head points to current node
(2) curr -> next = null // current node's next is set to null

newHead is passed to the last node of the call stack  
then, newHead keeps on the last node during the execution of the function

##### solve method
- first step: call stack recursively, to the last ListNode
- second step: perform the function, pop the stack, solve the subproblem step by step

```java
public ListNode reverse(ListNode head) {
    // a null list or a linkedlist with only 1 listnode
    if (head == null && head.next == null) {
        return head;
    }
    // point the next point of the head
    ListNode next = head.next;
    // complete the recursive subproblem
    ListNode newHead = reverse(next);
    next.next = head;
    head.next = null;
    return newHead;
}
```

### (2) find the middle point of the linkedlist

- for even number of listnodes, return the relatively former listnode of the linkedlist  
N1 -> N2 -> N3(prefer this position to be the middle point) -> N4 -> N5 -> N6 -> NULL

# 为什么去中点不是two pass, 而不是one pass #  
- if it is a data stream: can tell the middle point of the data stream at the earliest time
- two pass is offline algorithm, one pass is online algorithm  ASK THE INTERVIEWER!!!
- 数据量有多大，排好序了吗？优化什么内容(TC,SC)?

###（3）用快慢指针判断一个linkedlist是否有环。
快慢指针，是不是能到一个点

###（4）Insert a node in a sorted linked list (simple)

two common methods:
1. if-else 特殊判断
2. what's dummy head? When to use it？
- the head could be changed when solving the problem
- When we want to build a LinkedList from scratch (I don't know what should be the head initialy), i.e. merge two linkedlist


```java
Listnode dummyHead = new ListNode(-infinity);
dummyHead.next = newHead;

...

return dummyHead.next;
```
### (5) convert a LinkedList
N1 -> N2 -> N3 -> N4 -> N5 -> ... -> Nn -> null  (convert to)  
(N1 -> Nn) -> (N2 -> Nn-1) -> ...  

Step1: find one middle node
Step2: reverse the second half
Step3: merge the two lists (question 4 variant)  

### (6)partition sort
Given a linkedlist and a target value x, partition it such that all nodes less than x are listed
before the nodes larget than or equals to target value x.(keep the orginal relative order)

- step1: allocate two new linkedlists
- step2: iterate over the linkedlist, and compare the current node with the target
- step3: concatenate the tail of the small part to the head of the large part

### 举一反三
1. merge sort linked lists

2. add two numbers

342 + 465 = 807
input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
output: 7 -> 0 -> 8

follow up:
(1 -> 4 -> 3) + (5 -> 6 -> 4)
143 + 564 = 707
output： 707  

3. check if a linked list is palindrome
- find middle points
- reverse the second half
- compare the reverse one with the former lists

4. remove all nodes with target value
list = 2 -> 3 -> 6 -> 4 -> 6 -> null, target = 6
result: 2 -> 3 -> 4 -> null

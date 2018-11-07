## 1. Recusion
1. Surface: function call itself
2. Depth: Boil down a big problem to smaller ones.（n -> n - 1 -> ... -> n/2）
3. Implemenation:
a) base case: smaller problem to solve
b) recursive rule: how to make the tree smaller (if we can resolve the same problem with smaller size, then what is left to do for the current problem size n)

### example:
fibonacci: 有多少个点,分析node个个数  
- 时间复杂度：O（2^n）   
- 空间复杂度：返回的时候会释放内存，冯诺依曼体系结构。每次只能执行一条指令，每次在return的返回语句。  根据call stack，其实是树的高度决定了空间复杂度。O（logn）
- call stack:(n),之前都是n的
 can be regarded as a global accessible information that tells you what happened before each break point in each level.
- 每次减少问题的规模越大越好

## 2. Sort
### Selection Sort
- find the global min in the array, swap it with the first position
- find the global min in the rest of array. swap with the second position.
- ...

- In place Sort
#### 举一反二
- 放到stack中的做法，倒过来查询global min
- 如果有重复元素的话，可以加入一个counter记录元素个数

#### 举一反三
- 如何使用一个stack解决？

### Merge Sort
- merge: 谁小移谁
- Sort: -> 将更小的部分merge, 直到只有两个元素，直接排序
- 不断细分问题，然后merge到一起

Time Complexity:  
- 切分元素：O（n）
- merge：O（n * logn）:每层是logn

Space Complexity:
- space = n + n/2 + n/4 + ... + 1 = O(n)
>面试时候需要把自己推算TC, SC的过程描述出来，让面试者知道你是不是理解

####举一反二
Mergesort 用linkedList

Time Complexity:
- 切分元素： O（n * logn）
- merge：O(n * logn)

Space Complexity:
- 可以直接连起来，用linkedList连接一起
- O（logn）

- 实现A1B2C3D4到ABCD1234如何实现

### Quick Sort
- 选取一个位置，让小于它的在它左边，大于它的在它右边
- 两个挡板，三个区域思想
- set the pivot to the last position.
- use two points from the start and the end, move i and j to the center
- 挡板左侧比pivot小，右侧比pivot大，中间是待探索的区域，每次都这样做


#### worst case
Time Complexity：
average case: O(nlogn)
每一次都是选取到了最大/最小值，O(N^2)

Space Complexity:
average case: O(logn)
worst case: O(n)

#### 举一反二
把0放到最后面，把0作为挡板

#### 举一反三
rainbow sort
aaaa bbbb cccc
- 3个pointer: i,j,k
对于中间探索区域  
- case1: if input[j] == a; swap(i, j) i++, j++  
- case2: if input[j] == b; j++  
- case3: if input[j] == c; swap(j, k) k++

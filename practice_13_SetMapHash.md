# Set
## a collection that cannot contain duplicate elements

Three general-purpose Set implementations
- HashSet: which stores its elements in a hashtable, is the best-performing implementation; however it makes no guarantees concerning the order of iteration.
- TreeSet: which stores its elements in a red-black tree(balanced)
- LinkedHashSet: it is hashset and also it is a linkedlist, it maintains the order when each of the element is inserted into the HashSet.

put的值返回这个位置原来的值

#hashMap
###关于Object类hashCode()方法
>https://juejin.im/entry/5968876df265da6c232898c2

###HashMap vs. HashtTable


- hashtable:不允许key为null
- HashMap: 允许key为null

- hashtable:同步，性能相对较差
- hashMap:不同步，性能较好

### Collision control
- Collision - two keys mapped to the same bucket
    - Separate chaining(close addressing)
    - open addressing
        - remove（）可能要清理一些元素

###equals(), hashCode()
- 在找到对应的bucket之后，在linkedlist中不断应用equals()检验
- 两个元素hashCode()相同，两个元素不一定相同
- 两个元素相同，hashCode()一定相同
#### Principle
- In Java, there is a contract between equals() and hashCode(), the developers need to maintain:
1. If one.equals(two), it is a must that one.hashCode() == two.hashCode()
2. If one.hashCode() == two.hashCode(), it is not necessary one.equals(two)

###对于新建的类，比较相等的话需要同时override hashCode()和equals()方法
必须进入同一个bucket,->用hashcode完成，然后在list里面用equals找到对应元素

- hashCode()相同其实一定进入一个桶
- 进入一个桶，hashCode（）其实不一定相同

###hashCode()方法
`return a*31*31 + b.hashCode()*31 + c.hashCode()*1;`
primitive type是直接乘31， field是object就是用对应方法的HashCode()方法
有几个要加的field，就加入几个31进制


### Rehashing, load factor
溢出IDE，无所谓，执行就结果相同就可以

### hashset
底层是HashMap实现

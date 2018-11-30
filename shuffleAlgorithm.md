### Shuffle algorithm(洗牌算法)
```java
/*
Shuffle a set of numbers without duplicates.

Example:

// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
*/

class Solution {

    private int[] nums;
    private Random random;

    public Solution(int[] nums) {
        this.nums = nums;
        this.random = new Random();
    }

    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return nums;
    }

    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        if (nums == null) return null;
        int[] shuffle = nums.clone();
        for(int j = 1; j < shuffle.length; j++) {
            int i = random.nextInt(j + 1);
            swap(shuffle, i, j);
        }
        return shuffle;
    }

    public void swap(int[] array, int i, int j) {
        int temp = array[i];
        array[i] = array[j];
        array[j] = temp;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * Solution obj = new Solution(nums);
 * int[] param_1 = obj.reset();
 * int[] param_2 = obj.shuffle();
 */
```
### 对洗牌算法的证明
>https://www.geeksforgeeks.org/shuffle-a-given-array-using-fisher-yates-shuffle-algorithm/


>https://www.quora.com/Why-does-shuffling-array-by-iterating-over-it-and-swapping-it-with-a-random-element-between-0-to-the-last-element-of-the-array-not-produce-a-uniformly-distributed-shuffle


#### 给定一个长度为n的数组， 按照上述算法进行shuffle
想要证明每个位置都是等可能出现各个元素的 <=>  任何一个元素出现在第i个位置可能性都为  $\frac{ 1 }{ n }$  

1. 对于`index = n - 1`,最后一次swap的位置是针对倒数第一位置元素
- 任意一个元素达到最后一个元素的位置的概率是 $\frac{ 1 }{ n }$

2. 对于 `index = n - 2`, 要验证任意元素在倒数第二的位置的概率也是 $\frac{ 1 }{ n }$
- 首先对于 `index = n - 1`的最末端元素，到倒数第二个位置的概率是 $\frac{ 1 }{ n }$ ，在上文已经证明
- 对于`index = 0 ~index = n-2`元素
    - 在最后一次swap时候在该位置不被选中swap到最后的概率 $\frac{ n-1 }{ n }$
    - 在前面的`index = 0 ~index = n-2`元素中，被swap到倒数第二个点的位置的概率（swap倒数第二个点的位置时的操作）为 $\frac{ 1 }{ n - 1 }$
    - 上面2个概率相乘，得到前`index = 0 ~index = n-2`出现在倒数第二个点的位置的概率是  $\frac{ n-1 }{ n } * \frac{ 1 }{ n - 1 } = \frac{ 1 }{ n }$
- 综上，可以证明所有点到倒数第二个点的位置的概率都是 $\frac{ n-1 }{ n }$

3. 对于前面各点都可以进行上述证明，可以证明shuffle算法的有效性。

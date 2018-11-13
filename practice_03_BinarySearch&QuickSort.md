# Binary Search Practice
- Sorted Array
- Time Complexity: logn

## 1. Classic Binary Search
- No restrict for certain index (if exist more than one instance of the target value)
- sequence of thinking
  - understanding the question
  - go over the question with example and come up with algorithms
  - time and space complexity
  - coding


- definition: class is a noun, method is a verb
```java
public int binarySearch(int[] arr, int target) {
  // corner case
  if (arr == null || arr.length == 0) {
    return -1;
  }
  int left = 0;
  int right = arr.length - 1;
  int mid;
  while (left <= right) {
    mid = left + (right - left) / 2; // avoid overflow
    if (arr[mid] == target) {
      return mid;
    } else if(arr[mid] < target) {
      left = mid + 1;
    } else {
      right = mid - 1;
    }
  }
  return -1;
}
```

## 2.Closest In Sorted Array
- Must use `left + 1 < right` to avoid dead loop

```java
public int binarySearch(int[] arr, int target) {
    if (arr == null || arr.length == 0) return -1;
    int left = 0;
    int right = arr.length - 1;
    int mid;
    while (left + 1 < right) {
        mid = left + (left - right) / 2;
        if (arr[mid] == target) {
            return mid;
        } else if (arr[mid] < target) {
            left = mid;
        } else {
            right = mid;
        }
    }
    // post processing
    (Math.abs(arr[left] - target) <= Math.abs(arr[right] - target)) ? return left : return right;
}
```

## 3. K closest in sorted Array
Given a target integer T, a non-negative integer K and an integer array A sorted in ascending order, find the K closest numbers to T in A.
- Binary Seach + 反向移动挡板
- 找比target小的中最大的（等于） index = -1

```java
public class KClosest {
  public int[] kClosest(int[] array, int target, int k) {
    // corner cases
    if (array == null || array.length == 0) {
      return array;
    }   	
    if (k == 0) {
      return new int[0];
    }             
    // left is the index of the largest element smaller then target or equals to target,
    // right = left + 1
    // These two should be closest to target.
    int left = largestSmallerEqual(array, target);
    int right = left + 1;
    int[] result = new int[k];

    // this is a typical merge operation
    // priority: && is prior to ||
    for (int i = 0; i < k; i++) {
        // we can advance the left pointer when:
        // 1. right pointer is already out of bound
        // 2. right pointer is not out of bound, left pointer is not out of bound,
        // array[left] is closer to the target
        if (right >= array.length || (left >= 0
        && target - array[left] <= array[right] - target)) {
            result[i] = array[left--];
        } else {
            result[i] = array[right++];
        }
    }
  }			

  private int largestSmallerEqual(int[] array, int target) {
    // find the largest smaller or equal element's index in the Array
    int left = 0;
    int right = array.length - 1;
    while (left < right - 1) {
      int mid = left + (right - left) / 2;
      if (array[mid] <= target) {
          left = mid;
      } else {
          right = mid;
      }
    }
    if (array[right] <= target) {
        return right;
    }
    if(array[left] <= target) {
        return left;
    }
    // can't find...
    return -1;
  }
}
```

#  Quick Sort
TC:  
- average case: O(nlogn)
  - logn layer
  - every layer O(n)

- worse case: O(n^2)
  - n layer
  - every layer O(n)

SC:(call stack)  
- average case: logn
- worse case: n

```java
public class QuickSort {
    public int[] quickSort(int[] array) {
        // check null first
        if (array == null) {
            return array;
        }
        quickSort(array, 0, array.length - 1);
        return array;
    }

    public void quickSort(int[] array, int left, int right) {
        if (left >= right) {
            return;
        }
        // define a pivot and use the pivot to partition the array.
        int pivotPos = partition(array, left, right);
        // pivot is already at its position, when we do the recursive call on
        // the two partitions, pivot should not be included in any of them.
        quickSort(array, left, pivotPos - 1);
        quickSort(array, pivotPos + 1, right);
    }

    private int partition(int[] array, int left, int right) {
        int pivotIndex = pivotIndex(left, right);
        int pivot = array[pivotIndex];
        // swap the pivot element to the rightmost position first
        swap(array, pivotIndex, right);
        int leftBound = left;
        int rightBound = right - 1;
        while (leftBound <= rightBound) {
            if (array[leftBound] < pivot) {
                leftBound++;
            } else if (array[rightBound] >= pivot) {
                rightBound--;
            } else {
                swap(array, leftBound++, rightBound--); // switch the elements to the right sides
            }
        }
        // swap back the pivot element
        swap(array, leftBound, right);
        return leftBound;
    }

    // this is one of the ways defining the pivot,
    // pick random elements in the range of [left, right].
    private int pivotIndex(int left, int right) {
        return left + (int)(Math.random() * (right - left + 1));
    }

    private void swap(int[] array, int left, int right) {
        int temp = array[left];
        array[left] = array[right];
        array[right] = temp;
    }
}
```

# Rainbow Sort(extension of quick sort)
- corner case: j, k move to the same point, still need to swap, `while(zero <= one)`
- three

```java
/**
* Assumption:
* we have three colors denoted as -1, 0, 1 and all the elements in the array are valid;
*/
public class RainbowSort {
    public int[] rainbowSort(int[] array) {
        if (array == null || array.length <= 1) {
            return array;
        }
        // three bounds
        // 1. the left side of neg is all -1
        // 2. the right side of one is all 1
        // 3. the part between neg and zero is all 0
        // 4. between zero and one is to be discovered. (unknown)
        int neg = 0;
        int one = array.length - 1;
        int zero = 0;
        while (zero <= one) {
            if(array[zero] == -1) {
                swap(array, neg++, zero++);
            } else if (array[zero] == 0){
                zero++;
            } else {
                swap(array, zero, one--);
            }
        }
        return array;
    }

    private void swap(int[] array, int a, int b) {
        int tmp = array[a];
        array[a] = array[b];
        array[b] = tmp;
    }
}
```

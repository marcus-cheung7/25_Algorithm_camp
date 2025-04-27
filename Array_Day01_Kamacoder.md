# Array_Part01_Day01_Kamacoder

## 704. Binary Search

Given an array of integers `nums` sorted in ascending order, and an integer `target`, write a function to search for `target` in `nums`.  
If `target` exists, return its index. Otherwise, return -1.  
You must write an algorithm with O(log n) runtime complexity.

Use **binary search** to solve this problem.

```python
class Solution:
    def search(self, nums: List[int], target: int) -> int:
        left, right = 0, len(nums)
        while left < right:
            middle = (left + right) // 2
            if nums[middle] > target:
                right = middle
            elif nums[middle] < target:
                left = middle + 1
            else:
                return middle
        return -1
```

---

## 27. Remove Element

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in-place. The order of the elements may be changed.  
Then return the number of elements in `nums` which are not equal to `val`.

Consider the number of elements in `nums` which are not equal to `val` as `k`. To get accepted, you need to:

- Modify the array `nums` such that the first `k` elements contain the elements that are not equal to `val`.
- The remaining elements are not important, as well as the size of `nums`.
- Return `k`.

Use **two pointers** to solve this problem. Define two pointers, `slow` and `fast`, and move `fast` through the array:

- If `nums[fast]` is not equal to `val`, assign `nums[slow] = nums[fast]` and increment `slow` by 1.
- Always increment `fast` by 1.

At the end, `slow` will represent the number of elements not equal to `val`, and the modified array will contain these elements in its first `slow` positions.

```python
class Solution:
    def removeElement(self, nums: List[int], val: int) -> int:
        slow, fast = 0, 0
        n = len(nums)
        while fast < n:
            if nums[fast] != val:
                nums[slow] = nums[fast]
                slow += 1
            fast += 1
        return slow
```

---

## 977. Squares of a Sorted Array

Given an integer array `nums` sorted in **non-decreasing** order, return an array of the squares of each number, also sorted in **non-decreasing** order.

The approach is to first square each element in the array, then sort the resulting values in ascending order, and finally return the sorted array.  
Although the original array is sorted, squaring negative numbers can change the order of elements, so an additional sort is necessary to maintain non-decreasing order in the final result.

```python
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        for i in range(n):
            nums[i] *= nums[i]
        nums.sort()
        return nums
```

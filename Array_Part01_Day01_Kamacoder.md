# Array_Part01_Day01_Kamacoder
## 704.Binary Search
Given an array of integers nums which is sorted in ascending order, and an integer target, write a function to search target in nums. If target exists, then return its index. Otherwise, return -1.
You must write an algorithm with O(log n) runtime complexity.

Use "binary search" to solve this problem.
'''
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
'''

## 27.Remove Element
Given an integer array nums and an integer val, remove all occurrences of val in nums in-place. The order of the elements may be changed. Then return the number of elements in nums which are not equal to val.
Consider the number of elements in nums which are not equal to val be k, to get accepted, you need to do the following things:
Change the array nums such that the first k elements of nums contain the elements which are not equal to val. The remaining elements of nums are not important as well as the size of nums.
Return k.

Use "Two Pointers" to solve this problem, define two pointers as slow and fast. Then move fast through the array:
• If  '''nums[fast]''' is not equal to val, assign '''nums[slow] = nums[fast]''', and increment slow by 1.
• Always increment fast by 1.
At the end, slow will represent the number of elements not equal to val, and the modified array will contain these elements in its first slow positions.

'''
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
'''

## 977. Squares of a Sorted Array
Given an integer array '''nums''' sorted in **non-decreasing** order, return an array of the squares of each number sorted in **non-decreasing** order.

It first squares each element in the array, then sorts the resulting values in ascending order, and finally returns the sorted array. Although the original array is sorted, squaring negative numbers can change the order of elements, so an additional sort is necessary to maintain non-decreasing order in the final result.

'''
class Solution:
    def sortedSquares(self, nums: List[int]) -> List[int]:
        n = len(nums)
        for i in range(n):
            nums[i] *= nums[i]
        nums.sort()
        return nums
'''
# Array_Part01_Day01_Kamacoder
## 209. Minimum Size Subarray Sum
Given an array of positive integers `nums` and a positive integer `target`, return the **minimal length** of a subarray whose sum is greater than or equal to `target`. If there is no such subarray, return `0` instead.

Use **sliding window algorithm** （a kind of binary search）to solve this problem. The most important thing is to figure out what it exactly  is in `for j in nums`.

Solution 1
```
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        i = 0
        curr_sum = 0
        min_len = float('inf')
        
        for j in range(n):
            curr_sum += nums[j]
            
            while curr_sum >= target:
                subL = j - i + 1
                min_len = min(min_len, subL)
                curr_sum -= nums[i]
                i += 1
                
        return 0 if min_len == float('inf') else min_len
```
Better one:
``` 
class Solution:
    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        n = len(nums)
        i = 0
        j = 0
        min_len = float('inf')
        curr_sum = 0 
        while j < n:
            curr_sum += nums[j]
            
            while curr_sum >= target:
                min_len = min(min_len, j - i + 1)
                curr_sum -= nums[i]
                i += 1
            
            j += 1
        
        return min_len if min_len != float('inf') else 0
``` 
---
## 59. Spiral Matrix II
Given a positive integer `n`, generate an `n x n` `matrix` filled with elements from `1` to `n^2` in spiral order.

Initialize an `n x n` `matrix` filled with zeros and use variables `start_x` and `start_y` to track the starting point of each spiral layer. Then calculate the number of layers as `n // 2`, and use count to fill the numbers sequentially. For each layer, then move right across the top row, down along the right column, left across the bottom row, and up along the left column. After finishing a layer, then move the starting point inward. If `n` is odd, the center cell, which remains unfilled during the loops, is set separately at the end. This ensures that all numbers from `1` to `n^2` are placed in spiral order.
  
 ``` 
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[0] * n for _ in range(n)]
        start_x, start_y = 0, 0
        loop, mid = n // 2, n // 2
        count = 1

        for offset in range(1, loop + 1):
            for j in range(start_y, n - offset):
                matrix[start_x][j] = count
                count += 1
            for i in range(start_x, n - offset):
                matrix[i][n - offset] = count
                count += 1
            for j in range(n - offset, start_y, -1):
                matrix[n - offset][j] = count
                count += 1
            for i in range(n - offset, start_x, -1):
                matrix[i][start_y] = count
                count += 1
            start_x += 1
            start_y += 1

        if n % 2 != 0:
            matrix[mid][mid] = count
        return matrix
```
---
## KamaCoder 58. Range Sum
Given an integer array `Array`, calculate the total sum of elements within each specified interval.


```
import sys
input = sys.stdin.read

def main():
    data = input().split()
    index = 0
    n = int(data[index])
    index += 1
    vec = []
    for i in range(n):
        vec.append(int(data[index + i]))
    index += n

    p = [0] * n
    presum = 0
    for i in range(n):
        presum += vec[i]
        p[i] = presum

    results = []
    while index < len(data):
        a = int(data[index])
        b = int(data[index + 1])
        index += 2

        if a == 0:
            sum_value = p[b]
        else:
            sum_value = p[b] - p[a - 1]

        results.append(sum_value)

    for result in results:
        print(result)

if __name__ == "__main__":
    main()
```
---
## KamaCoder 44. Developer Land Purchase
In a city area divided into `n * m` contiguous blocks, each block has a different value representing its land worth. Currently, two development companies—`Company A` and `Company B`—are interested in purchasing the land in this city area.

The goal is to allocate all the blocks in the city area to either `Company A` or `Company B`.

However, due to urban planning restrictions, the area can only be divided horizontally or vertically into two subregions. Each subregion must contain one or more complete blocks—no further subdivision of individual blocks is allowed.

To ensure fair competition, your task is to determine a division method such that the difference in total land value between the two subregions assigned to `Company A` and `Company B` is minimized.

Note: Individual blocks cannot be split.

``` 
def main():
    import sys
    input = sys.stdin.read
    data = input().split()

    idx = 0
    n = int(data[idx])
    idx += 1
    m = int(data[idx])
    idx += 1
    sum = 0
    vec = []
    for i in range(n):
        row = []
        for j in range(m):
            num = int(data[idx])
            idx += 1
            row.append(num)
            sum += num
        vec.append(row)

    horizontal = [0] * n
    for i in range(n):
        for j in range(m):
            horizontal[i] += vec[i][j]

    vertical = [0] * m
    for j in range(m):
        for i in range(n):
            vertical[j] += vec[i][j]

    result = float('inf')
    horizontalCut = 0
    for i in range(n):
        horizontalCut += horizontal[i]
        result = min(result, abs(sum - 2 * horizontalCut))

    verticalCut = 0
    for j in range(m):
        verticalCut += vertical[j]
        result = min(result, abs(sum - 2 * verticalCut))

    print(result)

if __name__ == "__main__":
    main()
```
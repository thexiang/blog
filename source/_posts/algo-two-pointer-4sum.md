---
title: 4 Sum

categories:
- Alogrithm
- Two pointer
tags:
- Two pointer
---

https://www.lintcode.com/problem/58/

# Description
Given an array S of n integers, are there elements a, b, c, and d in S such that a + b + c + d = target?

Find all unique quadruplets in the array which gives the sum of target.

# Example
## Example 1:

Input:
numbers = [2,7,11,15]
target = 3

Output:
[]

Explanation:
2 + 7 + 11 + 15 != 3. There is no quadruple satisfying the condition.


## Example 2:

Input:
numbers = [1,0,-1,0,-2,2]
target = 0

Output:
[[-1, 0, 0, 1],[-2, -1, 1, 2],[-2, 0, 0, 2]]

Explanation:
There are three different quadruples whose sum of four numbers is 0.

# Solution
```python
from typing import (
    List,
)

class Solution:
    """
    @param numbers: Give an array
    @param target: An integer
    @return: Find all unique quadruplets in the array which gives the sum of zero
             we will sort your return value in output
    """
    def four_sum(self, numbers: List[int], target: int) -> List[List[int]]:
        # write your code here

        if not numbers:
            return []
        
        nums = sorted(numbers)
        results = []

        for i in range(len(nums)):
            if i > 0 and nums[i] == nums[i - 1]:
                continue
            for j in range(i+1, len(nums)):
                if j > i + 1 and nums[j] == nums[j - 1]:
                    continue

                pairs = self.find_two_sum_pairs(
                    nums,
                    j + 1,
                    len(nums) - 1,
                    target - nums[i] - nums[j],
                )

                for (c, d) in pairs:
                    results.append([nums[i], nums[j], c, d])
                
        return results

    
    def find_two_sum_pairs(self, nums, left, right, target):
        pairs = []
        while left < right:
            if nums[left] + nums[right] < target:
                left += 1
            elif nums[left] + nums[right] > target:
                right -= 1
            else:
                if not pairs or (nums[left], nums[right]) != pairs[-1]:
                    pairs.append((nums[left], nums[right]))
                left += 1
                right -= 1
        return pairs
```
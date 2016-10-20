Title: 238. Product of Array Except Self
Date: 2016-06-24 10:36:43
Category: LeetCode
Tags:
Slug: 238_Product_of_Array_Except_Self
Author: Lemon Tree

## Question

    Given an array of n integers where n > 1, nums, return an array output such that output[i] is equal to the product of all the elements of nums except nums[i].

    Solve it without division and in O(n).

    For example, given [1,2,3,4], return [24,12,8,6].

**Follow up**

    Could you solve it with constant space complexity? (Note: The output array does not count as extra space for the purpose of space complexity analysis.)


## Solution

值 = 所有左侧的数的乘积 * 所有右侧的数的乘积
可以用两个列表表示所有左侧数的乘积与右侧数的乘积。
给定数组[1, 2, 3, 4]
forward = [1, 1, 2, 6, 24]
backward = [1, 4, 12, 24, 24]
值 = forward[i] * backward[-(i+2)]

### Show me the code

```python
class Solution(object):
    def productExceptSelf(self, nums):
        """
        :type nums: List[int]
        :rtype: List[int]
        """

        nums_length = len(nums)
        forward, backward = [1], [1]
        for i in range(nums_length):
            forward.append(nums[i] * forward[i])
            backward.append(nums[-(i+1)] * backward[i])

        return [forward[x]*backward[-(x+2)] for x in range(nums_length)]
```

\- 完 -

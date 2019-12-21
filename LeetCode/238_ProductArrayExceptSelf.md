## LeetCode  238 除自身外数组的乘积
- 数组
- medium

### 描述
给定长度为 n 的整数数组 nums，其中 n > 1，返回输出数组 output ，其中 output[i] 等于 nums 中除 nums[i] 之外其余各元素的乘积。

示例:

输入: [1,2,3,4]
输出: [24,12,8,6]
说明: 请不要使用除法，且在 O(n) 时间复杂度内完成此题。

### 解答
从左到右遍历一遍数组，计算每个数左边的数的积，然后再从右到左遍历一遍数组，计算每个数右边的数的积，然后得出每个数除自己外的积。

```Python
class Solution:
    def productExceptSelf(self, nums: List[int]) -> List[int]:
        if not nums: return []
        ret = []
        p = 1
        for num in nums:
            ret.append(p)
            p *= num
        p = 1
        for i in range(len(nums)-1, -1, -1):
            ret[i] *= p
            p *= nums[i]
        return ret
```


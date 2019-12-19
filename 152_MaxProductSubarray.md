## LeetCode  152 最大乘积子数组
数组 动态规划
### 描述
给定一个整数数组 nums ，找出一个序列中乘积最大的连续子序列（该序列至少包含一个数）
示例 1:

输入: [2,3,-2,4]
输出: 6
解释: 子数组 [2,3] 有最大乘积 6。
示例 2:

输入: [-2,0,-1]
输出: 0
解释: 结果不能为 2, 因为 [-2,-1] 不是子数组。


### 解答
先假设全为非负数的情况，此时只要当前数不为0，则直接让之前的最大乘积乘上该数即可。
当有负数出现时，考虑到负数乘正数变负，负数乘负数变正的情况，可以用两个变量保存之前的结果，
一个保存之前的最大值，一个保存之前的最小值。当有负数出现时，翻转这两个中间结果。
需要注意的是，当有零出现时，需要清空之前的中间结果，重新开始算。

```Python
class Solution:
    def maxProduct(self, nums: List[int]) -> int: 
        ret = imin = imax = nums[0]
        for i in range(1, len(nums)):
            if nums[i] < 0:
                imin, imax = imax, imin
            imax = max(nums[i], nums[i] * imax)
            imin = min(nums[i], nums[i] * imin)
            ret = max(imax, ret)
        return ret
```
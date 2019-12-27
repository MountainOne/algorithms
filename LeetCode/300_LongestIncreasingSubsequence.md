## LeetCode  300 最长上升子序列
- 动态规划 数组
- hard

### 描述
给定一个无序的整数数组，找到其中最长上升子序列的长度。

示例:

输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
说明:

可能会有多种最长上升子序列的组合，你只需要输出对应的长度即可。
你算法的时间复杂度应该为 O(n2) 。
进阶: 你能将算法的时间复杂度降低到 O(n log n) 吗?

### 解答
二分加动态规划解决。`dp[i]`中的元素代表长度为 i 的递增子序列末尾元素的值，如果当前值大于该值，
则可以更新`dp[i+1]`的值，使用二分搜索加快查询速度。当 i 的值等于当前 size 时，将 size 加 1.

```Python
class Solution:
    def lengthOfLIS(self, nums: List[int]) -> int:
        if not nums: return 0
        dp = [0] * len(nums)
        size = 0
        for num in nums:
            i, j = 0, size
            while i != j:
                m = (i + j) // 2
                if num > dp[m]:
                    i = m + 1
                else:
                    j = m
            dp[i] = num
            size = max(size, i + 1)
        return size

```


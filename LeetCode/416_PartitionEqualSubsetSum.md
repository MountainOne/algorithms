## LeetCode  416  分割等和子集
- 动态规划
- medium

### 描述
给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

注意:

每个数组中的元素不会超过 100
数组的大小不会超过 200
示例 1:

输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
 

示例 2:

输入: [1, 2, 3, 5]

输出: false

解释: 数组不能分割成两个元素和相等的子集.

### 解答
0~1 背包问题的变种，在 dp 前需要求出背包负重，等于总和的一半，问题的求解就变成能否从数组中找到
总和等于该值的子集。状态转移方程为：`dp[i][j] = dp[i-1][j] or dp[i-1][j - nums[i-1]]`


```Python
class Solution:
    def canPartition(self, nums: List[int]) -> bool:
        if not nums: return False
        if sum(nums) % 2 != 0: return False
        half_sum = sum(nums) // 2
        n = len(nums)
        dp = [[False for _ in range(half_sum + 1)] \
              for i in range(n + 1)]
        for i in range(n + 1):
            dp[i][0] = True
        for i in range(1, n+1):
            for j in range(1, half_sum + 1):
                if j >= nums[i-1]:
                    dp[i][j] = dp[i-1][j] or dp[i-1][j - nums[i-1]]
        return dp[n][half_sum]
```


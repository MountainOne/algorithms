## LeetCode  279  完全平方数
- 动态规划
- medium

### 描述
给定正整数 n，找到若干个完全平方数（比如 1, 4, 9, 16, ...）使得它们的和等于 n。你需要让组成和的完全平方数的个数最少。

示例 1:

输入: n = 12
输出: 3 
解释: 12 = 4 + 4 + 4.
示例 2:

输入: n = 13
输出: 2
解释: 13 = 4 + 9.

### 解答
初始化条件为初始化长为 n + 1 的数组。状态转移方程为：`min_val = min(min_val, dp[i-j*j] + 1)`，
`dp[i]`等于所有加上一个合法平方数（小于 i）可达它的`dp[i-j*j]`中最小的那个加一。


```Python
class Solution:
    def numSquares(self, n: int) -> int:
        dp = [0 for _ in range(n+1)]
        for i in range(1, n+1):
            min_val = float('inf')
            j = 1
            while i >= j ** 2:
                min_val = min(min_val, dp[i-j*j] + 1)
                j += 1
            dp[i] = min_val
        return dp.pop()
```


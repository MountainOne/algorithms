## LeetCode  322  兑换零钱
- 动态规划
- medium

### 描述
给定不同面额的硬币 coins 和一个总金额 amount。编写一个函数来计算可以凑成总金额所需的最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回 -1。

示例 1:

输入: coins = [1, 2, 5], amount = 11
输出: 3 
解释: 11 = 5 + 5 + 1
示例 2:

输入: coins = [2], amount = 3
输出: -1
说明:
你可以认为每种硬币的数量是无限的。

### 解答
定义二维 dp 数组，`dp[i]`表示凑成金额 amount 所需的最少硬币数。状态转移方程为：
`dp[i] = min([dp[i-j] if i >= j else float('inf') for j in coins]) + 1`
当某种面额不可达时，会返回 inf。


```Python
class Solution:
    def coinChange(self, coins: List[int], amount: int) -> int:
        dp = [0] + [float('inf')] * amount
        for i in range(1, amount+1):
            dp[i] = min([dp[i-j] if i >= j else float('inf') for j in coins]) + 1
        return dp[amount] if dp[amount] != float('inf') else -1
```


## LeetCode  309  最佳买卖股票时机含冷冻期
- 动态规划
- medium

### 描述
给定一个整数数组，其中第 i 个元素代表了第 i 天的股票价格 。​

设计一个算法计算出最大利润。在满足以下约束条件下，你可以尽可能地完成更多的交易（多次买卖一支股票）:

你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。
卖出股票后，你无法在第二天买入股票 (即冷冻期为 1 天)。
示例:

输入: [1,2,3,0,2]
输出: 3 
解释: 对应的交易状态为: [买入, 卖出, 冷冻期, 买入, 卖出]

### 解答
跟直接买卖股票那道题不同的是，这道题有了冷冻期的概念。所以不能像直接买卖股票那道题一样简单地
累加所有能盈利的情况。
每一天都可能有三个状态：买入、卖出和冷静。其中买入状态，可由冷静状态买入股票和买入状态直接过渡；卖出状态只能由买入状态过渡；冷静状态可由卖出状态和冷静状态过渡。
每个状态都对应一个 dp 数组，数组值表示该天所获得的总利润。
计算每天三个状态的 dp 数组，最后返回冷静状态和卖出状态 dp 数组的最大值。

```Python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if not prices: return 0
        length = len(prices)
        s0 = [0 for _ in range(length)]
        s1 = [0 for _ in range(length)]        
        s2 = [0 for _ in range(length)]        
        s1[0] = -prices[0]
        s2[0] = float('-inf')
        for i in range(1, length):
            s0[i] = max(s0[i-1], s2[i-1])
            s1[i] = max(s0[i-1] - prices[i], s1[i-1])
            s2[i] = s1[i-1] + prices[i]
        return max(s0[length - 1], s2[length - 1])
```


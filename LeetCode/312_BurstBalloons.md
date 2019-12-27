## LeetCode  312  戳气球
- 动态规划
- hard

### 描述
有 n 个气球，编号为0 到 n-1，每个气球上都标有一个数字，这些数字存在数组 nums 中。

现在要求你戳破所有的气球。每当你戳破一个气球 i 时，你可以获得 nums[left] * nums[i] * nums[right] 个硬币。 这里的 left 和 right 代表和 i 相邻的两个气球的序号。注意当你戳破了气球 i 后，气球 left 和气球 right 就变成了相邻的气球。

求所能获得硬币的最大数量。

说明:

你可以假设 nums[-1] = nums[n] = 1，但注意它们不是真实存在的所以并不能被戳破。
0 ≤ n ≤ 500, 0 ≤ nums[i] ≤ 100
示例:

输入: [3,1,5,8]
输出: 167 
解释: nums = [3,1,5,8] --> [3,5,8] -->   [3,8]   -->  [8]  --> []
     coins =  3*1*5      +  3*5*8    +  1*3*8      + 1*8*1   = 167

### 解答
定义二维 dp 数组，`dp[i][j]`表示从 i 到 j 中间的气球全被戳破的情况下能拿到的最大分数。
状态转移方程为：` dp[left][right] = max(dp[left][right], \
                        dp[left][i] + dp[i][right] + nums[left]*nums[i]*nums[right])`
首先最外层循环定义间隔，从 2 开始（至少要戳破一个气球），然后定义左边界，根据间隔得到右边界，然后遍历中间的元素，得到 `dp[left][right]`。

```Python
class Solution:
    def maxCoins(self, nums: List[int]) -> int:
        if not nums: return 0
        nums = [1] + nums + [1]
        length = len(nums)
        dp = [[0] * length for _ in range(length)]
        for k in range(2, length):
            for left in range(length - k):
                right = left + k
                for i in range(left+1, right):
                    dp[left][right] = max(dp[left][right], \
                        dp[left][i] + dp[i][right] + nums[left]*nums[i]*nums[right])
        return dp[0][length-1]
```


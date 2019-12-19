## LeetCode  198 打家劫舍
动态规划
easy
### 描述
你是一个专业的小偷，计划偷窃沿街的房屋。每间房内都藏有一定的现金，影响你偷窃的唯一制约因素就是相邻的房屋装有相互连通的防盗系统，如果两间相邻的房屋在同一晚上被小偷闯入，系统会自动报警。

给定一个代表每个房屋存放金额的非负整数数组，计算你在不触动警报装置的情况下，能够偷窃到的最高金额。

示例 1:

输入: [1,2,3,1]
输出: 4
解释: 偷窃 1 号房屋 (金额 = 1) ，然后偷窃 3 号房屋 (金额 = 3)。
     偷窃到的最高金额 = 1 + 3 = 4 。
示例 2:

输入: [2,7,9,3,1]
输出: 12
解释: 偷窃 1 号房屋 (金额 = 2), 偷窃 3 号房屋 (金额 = 9)，接着偷窃 5 号房屋 (金额 = 1)。
     偷窃到的最高金额 = 2 + 9 + 1 = 12 。

### 解答
典型的动态规划题。状态转移函数为 `dp[i] = max(dp[i-2] + nums[i], dp[i-1])`。

```Python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) <= 0: return 0
        s0 = s1 = 0
        for i in range(len(nums)):
            tmp = s1
            s1 = max(s0 + nums[i], s1)
            s0 = tmp
        return s1
```
```Python
class Solution:
    def rob(self, nums: List[int]) -> int:
        if len(nums) <= 0: return 0
        if len(nums) == 1: return nums[0]
        if len(nums) == 2: return max(nums[0], nums[1])
        dp = [0] * len(nums)
        dp[0] = nums[0]
        dp[1] = max(nums[0], nums[1])
        for i in range(2, len(nums)):
            dp[i] = max(dp[i-2] + nums[i], dp[i-1])

        return max(dp[len(nums) - 1], dp[len(nums) - 2])
```
使用第一段代码，用时 48 ms，内存消耗 12.7 MB；
使用第二段代码，用时 28 ms，内存消耗 12.6 MB。
两段代码都是用 dp 做的，第二段代码更复杂，空间复杂度理论上为 O（N），而第一段代码的空间复杂度
为 O(1)。
为什么会造成这种情况呢？因为第一段代码在 for 循环里新建了变量 tmp，不停的创建和销毁对象会产生极大的开销，所以第一段代码正确的做法应该是把 tmp 放在循环外，只创建一次。修改后的算法只用了 24 ms。
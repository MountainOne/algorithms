## LeetCode  494  目标和
- 动态规划
- medium

### 描述
给定一个非负整数数组，a1, a2, ..., an, 和一个目标数，S。现在你有两个符号 + 和 -。对于数组中的任意一个整数，你都可以从 + 或 -中选择一个符号添加在前面。

返回可以使最终数组和为目标数 S 的所有添加符号的方法数。

示例 1:

输入: nums: [1, 1, 1, 1, 1], S: 3
输出: 5
解释: 

-1+1+1+1+1 = 3
+1-1+1+1+1 = 3
+1+1-1+1+1 = 3
+1+1+1-1+1 = 3
+1+1+1+1-1 = 3

一共有5种方法让最终目标和为3。
注意:

数组非空，且长度不会超过20。
初始的数组的和不会超过1000。
保证返回的最终结果能被32位整数存下。

### 解答
状态转移方程为：` tdic[d + nums[i]] = tdic.get(d + nums[i], 0) + dic.get(d, 0)
                tdic[d - nums[i]] = tdic.get(d - nums[i], 0) + dic.get(d, 0)`
每次遍历时，通过之前得到的所有数加减当前数得到新的数，新的数的路径和，即为所能到达该数的路径和之和。
注意在初始化第一个数时，如果第一个数为 0，则字典初始化为`{0 : 2}`，否则为`{nums[0] : 1, -nums[0] : 1}`，因为只有第一个数进行的是一元计算。
每次遍历新数时都要新建字典，因为必须确保本轮所得的数是由前一轮通过加减得到的，而不能是之前的轮次。


```Python
class Solution:   
   def findTargetSumWays(self, nums: List[int], S: int) -> int:
        if not nums:
            return 0
        dic = {nums[0]: 1, -nums[0]: 1} if nums[0] != 0 else {0: 2}
        for i in range(1, len(nums)):
            tdic = {}
            for d in dic:
                tdic[d + nums[i]] = tdic.get(d + nums[i], 0) + dic.get(d, 0)
                tdic[d - nums[i]] = tdic.get(d - nums[i], 0) + dic.get(d, 0)
            dic = tdic
        return dic.get(S, 0)
        
```


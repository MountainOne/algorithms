## LeetCode  239  滑动窗口的最大值
- 堆
- hard

### 描述
给定一个数组 nums，有一个大小为 k 的滑动窗口从数组的最左侧移动到数组的最右侧。你只可以看到在滑动窗口内的 k 个数字。滑动窗口每次只向右移动一位。

返回滑动窗口中的最大值。

### 解答
从左到右遍历一遍数组，取滑动窗口最大值即可。有一个优化的方法是，用一个变量保存当前窗口的和，在每到
一个新的窗口时，加上最新的数，减掉上一个窗口最前的数，这样就避免了每到一个新窗口都要重头计算。


```Python
class Solution:
    def maxSlidingWindow(self, nums: List[int], k: int) -> List[int]:
        if not nums: return []
        ret = [max(nums[i:i+k]) for i in range(len(nums) - k + 1)]
        return ret
```


## LeetCode  448  找到数组中所有消失的数字
- 数组
- easy

### 描述
给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:

输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]

### 解答
因为所有的数都不会超过数组长度大小 n，所以可以在第一次遍历数组时，将值对应的索引位置置为负数，
在第二次遍历时只需要将所有为正的索引输出即可。


```Python
class Solution:
    def findDisappearedNumbers(self, nums: List[int]) -> List[int]:
        if not nums: return []
        for i in range(len(nums)):
            index = abs(nums[i]) - 1
            nums[index] = -abs(nums[index])
        return [i + 1 for i in range(len(nums)) if nums[i] > 0]
```


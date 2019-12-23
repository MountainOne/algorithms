## LeetCode  283  移动零
- 数组
- easy

### 描述
给定一个数组 nums，编写一个函数将所有 0 移动到数组的末尾，同时保持非零元素的相对顺序。

示例:

输入: [0,1,0,3,12]
输出: [1,3,12,0,0]
说明:

必须在原数组上操作，不能拷贝额外的数组。
尽量减少操作次数。

### 解答
初始化一个索引和一个计数器，遍历时遇到 0 则计数器加一，弹出 list 中的 0.没有遇到 0 则索引加一。
遍历结束后在 list 末尾补 0.


```Python
class Solution:
    def moveZeroes(self, nums: List[int]) -> None:
        """
        Do not return anything, modify nums in-place instead.
        """
        if not nums: return 
        cnt, index = 0, 0
        while index < len(nums):
            if nums[index] == 0:
                nums.pop(index)
                cnt += 1
            else:
                index += 1
        nums.extend([0] * cnt)
```


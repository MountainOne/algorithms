## LeetCode  287  寻找重复数
- 数组
- 中等

### 描述
给定一个包含 n + 1 个整数的数组 nums，其数字都在 1 到 n 之间（包括 1 和 n），可知至少存在一个重复的整数。假设只有一个重复的整数，找出这个重复的数。

示例 1:

输入: [1,3,4,2,2]
输出: 2
示例 2:

输入: [3,1,3,4,2]
输出: 3
说明：

不能更改原数组（假设数组是只读的）。
只能使用额外的 O(1) 的空间。
时间复杂度小于 O(n2) 。
数组中只有一个重复的数字，但它可能不止重复出现一次。

### 解答
这题有一个条件就是数组中的数字都在 1 到 n 之间，这意味着数组的索引和值的最大值相等。我们可以
用这个数组来模拟链表的结构，将判断重复数的问题转换为判断链表中环的位置的问题。具体通过，准备一个
快指针一个慢指针，快指针每次移动两格，慢指针每次移动一格。当两个指针第一次相遇的时候，暂停循环，重置快指针。然后让两个指针以每次一格的频率移动，再次相遇的位置即为环的位置，也即重复的数字。


```Python
class Solution:
    def findDuplicate(self, nums: List[int]) -> int:
        if not nums: return 0
        slow = fast = nums[0]
        
        while True:
            slow = nums[slow]
            fast = nums[nums[fast]]
            if fast == slow:
                break
        fast = nums[0]
        while fast != slow:
            slow = nums[slow]
            fast = nums[fast]
        return slow
```


## LeetCode  581  最短无序连续子数组
- 数组
- easy

### 描述
给定一个整数数组，你需要寻找一个连续的子数组，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是最短的，请输出它的长度。

示例 1:

输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
说明 :

输入的数组长度范围在 [1, 10,000]。
输入的数组可能包含重复元素 ，所以升序的意思是<=。

### 解答
第一次从左到右遍历数组，找到第一个上升沿之后的最小值 mi；第二次从右到左遍历数组，找到第一个
下降沿后的最大值 ma。第三次从左到右遍历数组，找到第一个大于 mi 的值的位置为左边界；第四次从右
到左遍历数组，找到第一个小于ma 的值的位置作为右边界，然后返回该无序数组的长度。
其原理在于最大限度的利用左右边界处已经排序好的部分。


```Python
class Solution:
    def findUnsortedSubarray(self, nums: List[int]) -> int:
        if not nums: return 0
        flag = False
        mi = float('inf') 
        ma = float('-inf')
        for i in range(1, len(nums)):
            if nums[i] < nums[i-1]:
                flag = True
            if flag:
                mi = min(mi, nums[i])
        flag = False
        for i in range(len(nums)-2, -1, -1):
            if nums[i] > nums[i+1]:
                flag = True
            if flag:
                ma = max(ma, nums[i])
        l = r = 0
        for i in range(len(nums)):
            if nums[i] > mi:
                l = i
                break
        for i in range(len(nums)-1, -1, -1):
            if nums[i] < ma:
                r = i
                break
        return r - l + 1 if r - l > 0 else 0
                
            
```


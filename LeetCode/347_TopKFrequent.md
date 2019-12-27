## LeetCode  347  前 k 个高频元素
- 堆
- medium

### 描述
给定一个非空的整数数组，返回其中出现频率前 k 高的元素。

示例 1:

输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
示例 2:

输入: nums = [1], k = 1
输出: [1]
说明：

你可以假设给定的 k 总是合理的，且 1 ≤ k ≤ 数组中不相同的元素的个数。
你的算法的时间复杂度必须优于 O(n log n) , n 是数组的大小。

### 解答
利用 python 自带的容器 Counter 求解。


```Python
class Solution:
    def topKFrequent(self, nums: List[int], k: int) -> List[int]:
        if not nums: return []
        counter = collections.Counter(nums)
        common = counter.most_common(k)
        ret = [common[i][0] for i in range(len(common))]
        return ret
```


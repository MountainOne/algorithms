## LeetCode  215 数组中的第 k 个最大元素
堆
medium

### 描述
在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:

输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
示例 2:

输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
说明:

你可以假设 k 总是有效的，且 1 ≤ k ≤ 数组的长度。

### 解答
可以直接将整个数组排序后直接取出第 k 大的元素，这种方法的时间复杂度为 O(NlogN)。
更加优秀的做法是构建一个最小根堆，然后 pop 出 len - k 个元素，得到第 k 大的元素，时间复杂度
接近 O(N)。

```Python
class Solution:
    def findKthLargest(self, nums: List[int], k: int) -> int:
        heap = []
        for i in range(len(nums)):
            heapq.heappush(heap, nums[i])
        for _ in range(len(nums) - k):
            heapq.heappop(heap)
        return heapq.heappop(heap)
```


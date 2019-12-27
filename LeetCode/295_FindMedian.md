## LeetCode  295 数据流中的中位数
- 堆 设计
- hard

### 描述
中位数是有序列表中间的数。如果列表长度是偶数，中位数则是中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。
示例：

addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
进阶:

如果数据流中所有整数都在 0 到 100 范围内，你将如何优化你的算法？
如果数据流中 99% 的整数都在 0 到 100 范围内，你将如何优化你的算法？

### 解答
构建两个小根堆`small`和`large`，其中 `small` 中存的是负数。`large`中堆顶是堆中最小值，`small`中堆顶是堆中绝对值最大值。每次插入值时，如果两个堆大小相等，则大根堆插入值，如果大小不等，则小根堆插入值。每次插入时，都需要把插入元素先 push 进另一个堆里，然后再从另一个堆里 pop 出堆顶元素插入。这样保证了最终插入堆的元素在全局中处于中间位置，确保了每次返回堆顶元素时，返回的是位于中间位置的元素。
每次返回时，若两堆大小不等，则返回`large`的堆顶元素，否则返回两个堆堆顶元素的均值。

当所有整数都在 0 到 100 范围内时，可以考虑用一个包含 100 个元素的数组统计每个数出现的次数，在需要查询中值时，根据当前总数是奇数还是偶数，返回对应的中值。
当数据流中 99% 的整数都在 0 到 100 范围内时，单独用一个变量记录不在 0 到 100 范围内的，其余操作同上。




```Python
from heapq import *
class MedianFinder:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.small = []
        self.large = []

    def addNum(self, num: int) -> None:
        if len(self.small) == len(self.large):
            heappush(self.large, -heappushpop(self.small, -num))
        else:
            heappush(self.small, -heappushpop(self.large, num))

    def findMedian(self) -> float:
        if len(self.small) == len(self.large):
            return float((self.large[0] - self.small[0]) / 2)
        else:
            return float(self.large[0])
```


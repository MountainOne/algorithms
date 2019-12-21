## LeetCode  169 多数元素
数组 位运算
easy
### 描述
给定一个大小为 n 的数组，找到其中的多数元素。多数元素是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

示例 1:

输入: [3,2,3]
输出: 3
示例 2:

输入: [2,2,1,1,1,2,2]
输出: 2

### 解答
《剑指 offer》上有一道“寻找水王”的题和该题类似，可以用一个计数器表示某个数出现的次数。在循环中，
出现该数时，计数器加一，未出现时减一。当计数器被减为 0 时，修改计数器对应的数，并重新记次数。

```Python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        cnt = 1
        num = nums[0]
        for i in range(1, len(nums)):
            if nums[i] == num:
                cnt += 1
            else:
                if cnt <= 0:
                    cnt = 1
                    num = nums[i]
                else:
                    cnt -= 1
        return num
```
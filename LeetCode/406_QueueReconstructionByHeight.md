## LeetCode  406  根据身高重建队列
- 贪心 数组
- medium

### 描述
假设有打乱顺序的一群人站成一个队列。 每个人由一个整数对(h, k)表示，其中h是这个人的身高，k是排在这个人前面且身高大于或等于h的人数。 编写一个算法来重建这个队列。

注意：
总人数少于1100人。

示例

输入:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

输出:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]

### 解答
首先构建每种身高的人的字典，键是身高，值是一个二元组，第一个元素是他前面有多少人，第二个元素是在原数组中的位置。同时构建有多少种身高的数组。然后对身高数组排序，身高从大到小遍历，往 ret 数组中插入对应原数组位置的值。
由于是从大到小进行插入，所以可以确保顺序是正确的。


```Python
class Solution:
    def reconstructQueue(self, people: List[List[int]]) -> List[List[int]]:
        if not people: return None
        peopledict, heights, ret = {}, [], []
        for i in range(len(people)):
            p = people[i]
            if p[0] in peopledict:
                peopledict[p[0]].append((p[1], i))
            else:
                peopledict[p[0]] = [(p[1], i)]
                heights.append(p[0])
        heights.sort()
        for height in heights[::-1]:
            peopledict[height].sort()
            for p in peopledict[height]:
                ret.insert(p[0], people[p[1]])
        return ret
```


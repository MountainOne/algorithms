## LeetCode  207 课程调度
图
medium

### 描述
现在你总共有 n 门课需要选，记为 0 到 n-1。

在选修某些课程之前需要一些先修课程。 例如，想要学习课程 0 ，你需要先完成课程 1 ，我们用一个匹配来表示他们: [0,1]

给定课程总量以及它们的先决条件，判断是否可能完成所有课程的学习？

示例 1:

输入: 2, [[1,0]] 
输出: true
解释: 总共有 2 门课程。学习课程 1 之前，你需要完成课程 0。所以这是可能的。
示例 2:

输入: 2, [[1,0],[0,1]]
输出: false
解释: 总共有 2 门课程。学习课程 1 之前，你需要先完成​课程 0；并且学习课程 0 之前，你还应先完成课程 1。这是不可能的。
说明:

输入的先决条件是由边缘列表表示的图形，而不是邻接矩阵。详情请参见图的表示法。
你可以假定输入的先决条件中没有重复的边。

### 解答
图相关的题目都要构建两个数组，一个是图数组，另一个是每个点是否可达的数组。本题可以看做判断
图中是否出现了环，如果出现了环，则返回 false，否则返回 true。
dfs 的逻辑是：
1.如果当前点可达，返回 True
2.如果当前点不可达，返回 False
3.令`visit[i] = -1`，对 i 所有的邻接点调用`dfs()`，如果有一个点返回 False，则返回 False。
需要注意的是，在一开始就将`visit[i] = -1`，这样当第二次搜索这个点时，就可以直接返回 false 了。

```Python
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        graph = [[] for _ in range(numCourses)]
        visit = [0 for _ in range(numCourses)]
        for x, y in prerequisites:
            graph[x].append(y) 
        
        def dfs(i):
            if visit[i] == -1: return False
            elif visit[i] == 1: return True
            else:
                visit[i] = -1
                for j in graph[i]:
                    if not dfs(j):
                        return False
                visit[i] = 1
                return True
                
        for i in range(numCourses):
            if not dfs(i):
                return False
        return True
```


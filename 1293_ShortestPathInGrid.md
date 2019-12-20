## LeetCode  1293 网格中的最短路径
- 数组
- medium

### 描述
给你一个 m * n 的网格，其中每个单元格不是 0（空）就是 1（障碍物）。每一步，您都可以在空白单元格中上、下、左、右移动。

如果您 最多 可以消除 k 个障碍物，请找出从左上角 (0, 0) 到右下角 (m-1, n-1) 的最短路径，并返回通过该路径所需的步数。如果找不到这样的路径，则返回 -1。

示例 1：

输入： 
grid = 
[[0,0,0],
 [1,1,0],
 [0,0,0],
 [0,1,1],
 [0,0,0]], 
k = 1
输出：6
解释：
不消除任何障碍的最短路径是 10。
消除位置 (3,2) 处的障碍后，最短路径是 6 。该路径是 (0,0) -> (0,1) -> (0,2) -> (1,2) -> (2,2) -> (3,2) -> (4,2).

### 解答
稍微复杂化的广度优先搜索。由于在最短路径中显然不会经过同一位置超过一次，因此最多消除 k 个障碍物，等价经过 k 个障碍物。所以就可以用(x, y, rest)这个三元组表示一个搜索状态，其中(x, y)表示玩家的位置，rest 表示玩家还可以经过多少个障碍物，它的值必须为非负数。然后就分情况讨论当前位置是否为障碍物即可。
有一个优化点在于，k 的上限为 m*n，可以直接选择直线从上到下，再从下往右的路线，这样的距离为 m+n-1,最多遇到 m+n-3个障碍物，所以可以将 k 的值设为 `min(k, m+n-3)`。

```Python
class Solution:
    def shortestPath(self, grid: List[List[int]], k: int) -> int:
        if not grid: return 0
        m, n = len(grid), len(grid[0])
        if m == 1 and n == 1: return 0
        k = min(k, m + n - 3)
        visited = set([(0, 0, k)]) 
        q = collections.deque([(0, 0, k)])
        step = 0
        while len(q) > 0:
            step += 1
            cnt = len(q)
            for _ in range(cnt):
                x, y, rest = q.popleft()
                for dx, dy in [(-1, 0), (1, 0), (0, -1), (0, 1)]:
                    nx, ny = x + dx, y + dy
                    if 0 <= nx < m and 0 <= ny < n:
                        if grid[nx][ny] == 0 and (nx, ny, rest) not in visited:
                            if nx == m - 1 and ny == n - 1:
                                return step
                            q.append((nx, ny, rest))
                            visited.add((nx, ny, rest))
                        elif grid[nx][ny] == 1 and rest > 0 and (nx, ny, rest - 1) not in visited:
                            q.append((nx, ny, rest - 1))
                            visited.add((nx, ny, rest - 1))
        return -1
```


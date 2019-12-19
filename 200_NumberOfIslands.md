## LeetCode  200 岛屿数量
图
medium
### 描述
给定一个由 '1'（陆地）和 '0'（水）组成的的二维网格，计算岛屿的数量。一个岛被水包围，并且它是通过水平方向或垂直方向上相邻的陆地连接而成的。你可以假设网格的四个边均被水包围。

示例 1:

输入:
11110
11010
11000
00000

输出: 1
示例 2:

输入:
11000
11000
00100
00011

输出: 3
### 解答
深度优先搜索和广度优先搜索都可以。这里可以在搜索的时候，将已经搜过的位置置为 0，这样就避免了再新建一个
表示位置状态的数组。

```Python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        if not grid: return 0
        cnt = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == '1':
                    self.dfs(grid, i, j)
                    cnt += 1
        return cnt
    
    def dfs(self, grid, i, j):
        if i < 0 or j < 0 or i >= len(grid) or j >= len(grid[0]) \
            or grid[i][j] == '0':
            return 
        grid[i][j] = '0'
        self.dfs(grid, i+1, j)
        self.dfs(grid, i, j+1)        
        self.dfs(grid, i-1, j)        
        self.dfs(grid, i, j-1)   
```


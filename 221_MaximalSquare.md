## LeetCode  221 最大正方形
- 动态规划
- medium

### 描述
在一个由 0 和 1 组成的二维矩阵内，找到只包含 1 的最大正方形，并返回其面积。

示例:

输入: 

1 0 1 0 0
1 0 1 1 1
1 1 1 1 1
1 0 0 1 0

输出: 4


### 解答
经典的动态规划问题。初始化操作为构建一个与`matrix`完全一致的 `dp`矩阵。
状态转移方程为：`dp[i][j] = min(dp[i-1][j], dp[i][j-1]，v
                        dp[i-1][j-1]) + 1`
`dp[i][j]`表示某点能表示的最大正方形的边长。当 `matrix[i][j]`为 1 时，由左上、上、左三个点的
状态加一得到，否则为 0。在求出 dp 矩阵后，遍历 dp 矩阵得到最大值，然后求出最大正方形的面积。

```Python
class Solution:
    def maximalSquare(self, matrix: List[List[str]]) -> int:
        if not matrix: return 0
        high, width = len(matrix), len(matrix[0])
        dp = [[0 if matrix[i][j] == '0' else 1 \
               for j in range(width)] for i in range(high)]
        for i in range(1, high):
            for j in range(1, width):
                if matrix[i][j] == '1':
                    dp[i][j] = min(dp[i-1][j], dp[i][j-1], \
                        dp[i-1][j-1]) + 1
                else:
                    dp[i][j] = 0
        res = max(max(row) for row in dp)
        return res ** 2
```


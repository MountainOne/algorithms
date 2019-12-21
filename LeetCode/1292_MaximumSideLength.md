## LeetCode  1292 元素和小于等于阈值的正方形的最大边长
- 数组
- medium

### 描述
给你一个大小为 m x n 的矩阵 mat 和一个整数阈值 threshold。

请你返回元素总和小于或等于阈值的正方形区域的最大边长；如果没有这样的正方形区域，则返回 0 。

输入：mat = [[1,1,3,2,4,3,2],[1,1,3,2,4,3,2],[1,1,3,2,4,3,2]], threshold = 4
输出：2
解释：总和小于 4 的正方形的最大边长为 2。

### 解答
利用前缀和数组实现快速的计算矩阵的元素和。然后在遍历时，当出现大于边长 c 的正方形时，在
之后的遍历中就不用考虑边长它小的情况了。

```Python
class Solution:
    def maxSideLength(self, mat: List[List[int]], threshold: int) -> int:
        m, n = len(mat), len(mat[0])
        P = [[0] * (n + 1) for _ in range(m + 1)]
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                P[i][j] = P[i - 1][j] + P[i][j - 1] - P[i - 1][j - 1] + mat[i - 1][j - 1]
        
        def getRect(x1, y1, x2, y2):
            return P[x2][y2] - P[x1 - 1][y2] - P[x2][y1 - 1] + P[x1 - 1][y1 - 1]
        
        r, ans = min(m, n), 0
        for i in range(1, m + 1):
            for j in range(1, n + 1):
                for c in range(ans + 1, r + 1):
                    if i + c - 1 <= m and j + c - 1 <= n and getRect(i, j, i + c - 1, j + c - 1) <= threshold:
                        ans += 1
                    else:
                        break
        return ans
```


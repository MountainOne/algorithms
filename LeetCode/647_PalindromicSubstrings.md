## LeetCode  647  回文子串
- 字符串 动态规划
- medium

### 描述
给定一个字符串，你的任务是计算这个字符串中有多少个回文子串。

具有不同开始位置或结束位置的子串，即使是由相同的字符组成，也会被计为是不同的子串。

示例 1:

输入: "abc"
输出: 3
解释: 三个回文子串: "a", "b", "c".
示例 2:

输入: "aaa"
输出: 6
说明: 6个回文子串: "a", "a", "a", "aa", "aa", "aaa".
注意:

输入的字符串长度不会超过1000。

### 解答
manacher 算法计算回文子串。
1.在原字符串首尾分别填充“@#”和“#$”，然后在每个字符间填充"#"，这样是为了避免奇偶回文串的影响
2.初始化 z 数组，记录每个字符的最大回文串数。初始化 center 和 right，记录当前最右侧的回文串中心
和最远右边距
3.遍历字符串，如果当前位置小于 right，则初始化 ` Z[i] = min(right - i, Z[2 * center - i])`
避免重复计算，然后往左右延伸，知道两侧不相等。
4.如果当前回文串最右端大于 right，则更新 center 和 right。
5.返回 Z 数组。

```Python
class Solution:
    def countSubstrings(self, s: str) -> int:
        def manachers(S):
            A = '@#' + '#'.join(S) + '#$'
            Z = [0] * len(A)
            center = right = 0
            for i in range(1, len(A) - 1):
                if i < right:
                    Z[i] = min(right - i, Z[2 * center - i])
                while A[i + Z[i] + 1] == A[i - Z[i] - 1]:
                    Z[i] += 1
                if i + Z[i] > right:
                    center, right = i, i + Z[i]
            return Z

        return sum((v+1)//2 for v in manachers(s))     
```


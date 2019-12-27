## LeetCode  438  找到字符串中的所有字母异位词
- 字符串
- medium

### 描述
给定一个字符串 s 和一个非空字符串 p，找到 s 中所有是 p 的字母异位词的子串，返回这些子串的起始索引。

字符串只包含小写英文字母，并且字符串 s 和 p 的长度都不超过 20100。

说明：

字母异位词指字母相同，但排列不同的字符串。
不考虑答案输出的顺序。
示例 1:

输入:
s: "cbaebabacd" p: "abc"

输出:
[0, 6]

解释:
起始索引等于 0 的子串是 "cba", 它是 "abc" 的字母异位词。
起始索引等于 6 的子串是 "bac", 它是 "abc" 的字母异位词。
 示例 2:

输入:
s: "abab" p: "ab"

输出:
[0, 1, 2]

解释:
起始索引等于 0 的子串是 "ab", 它是 "ab" 的字母异位词。
起始索引等于 1 的子串是 "ba", 它是 "ab" 的字母异位词。
起始索引等于 2 的子串是 "ab", 它是 "ab" 的字母异位词。

### 解答
用两个 Counter 依次对比记录即可。


```Python
from collections import Counter
class Solution:
    def findAnagrams(self, s: str, p: str) -> List[int]:
        if not s or not p: return []
        ret = []
        p_len = len(p)
        sCounter = Counter(s[:p_len-1])
        pCounter = Counter(p)
        for i in range(p_len-1, len(s)):
            sCounter[s[i]] += 1
            if sCounter == pCounter:
                ret.append(i-p_len+1)
            sCounter[s[i-p_len+1]] -= 1
            if sCounter[s[i-p_len+1]] == 0:
                del sCounter[s[i-p_len+1]]
        return ret
```


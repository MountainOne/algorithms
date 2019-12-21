## LeetCode 139 Word Break
Topics: DP
### Description

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

Note:

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.
Example 1:
> Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".

Example 2:
> Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
             
Example 3:
> Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
### Solution
对于当前索引 i 的状态，如果它之前的某个状态 j 可以被划分，那么只要判断 j 到 i 的这个单词是否在 wordDict 里，就可以确定状态 i 也是可以被划分的。

```Python
class Solution:
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        dp = [False] * (len(s) + 1)
        dp[0] = True
        for i in range(1, len(s) + 1):
            for j in range(i):
                if dp[j] and (s[j: i] in wordDict):                    
                    dp[i] = True
                    break
        return dp[len(s)]
```

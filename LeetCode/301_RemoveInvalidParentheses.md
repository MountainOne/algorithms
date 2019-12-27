## LeetCode  301 删除无效括号
- 字符串
- hard


### 描述
删除最小数量的无效括号，使得输入的字符串有效，返回所有可能的结果。

说明: 输入可能包含了除 ( 和 ) 以外的字符。

示例 1:

输入: "()())()"
输出: ["()()()", "(())()"]
示例 2:

输入: "(a)())()"
输出: ["(a)()()", "(a())()"]
示例 3:

输入: ")("
输出: [""]

### 解答
判断当前的括号是否有效是通过当前左括号的数量是否大于等于右括号的数量，如果小于则当前括号无效。
从左到右遍历字符串，当出现无效的情况时，删除无效的右括号。删除的右括号索引应从上一次删除的索引处开始，
避免重复删除连续的右括号，对于连续的右括号，只需要删除第一个右括号即可。
在递归的过程中需要记录两个索引，一个是进行递归时字符串当前的索引，使得下一次递归直接从当前位置开始；另一个是删除的无效括号的索引，使得下一次删除时从该位置开始，避免重复删除。
当从左到右检测完所有的无效右括号时，将字符串反转，检测左括号。此时需要将一开始传入的 pair 列表反转一下。

```Python
class Solution:
    def removeInvalidParentheses(self, s: str) -> List[str]:
        if not s: return [""]
        ret = []
        self.remove(s, ret, 0, 0, ['(', ')'])
        return ret
    
    def remove(self, s, ret, last_delete_index, last_index, pair):
        cnt = 0
        for i in range(last_index, len(s)):
            if s[i] == pair[0]:
                cnt += 1
            elif s[i] == pair[1]:
                cnt -= 1
            if cnt >= 0: continue
            for j in range(last_delete_index, i+1):
                if s[j] == pair[1] and (j == last_delete_index or s[j-1] != pair[1]):
                    self.remove(s[:j]+s[j+1:], ret, j, i, pair)
            return
        s_revert = s[::-1]
        if pair[0] == '(':
            self.remove(s_revert, ret, 0, 0, [')', '('])
        else:
            ret.append(s_revert)
```


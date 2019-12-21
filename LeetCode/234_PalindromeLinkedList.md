## LeetCode  234 回文链表
- 链表
- easy

### 描述
请判断一个链表是否为回文链表。


### 解答
从链表的中间位置开始，分别向两侧遍历，如果相等则继续循环，不相等则返回 false。

```Python
class Solution:
    def isPalindrome(self, head: ListNode) -> bool:
        rev = None
        fast = head
        while fast and fast.next:
            fast = fast.next.next
            rev, rev.next, head = head, rev, head.next
        tail = head.next if fast else head
        isPali = True
        while rev:
            isPali = isPali and rev.val == tail.val
            head, head.next, rev = rev, head, rev.next
            tail = tail.next
        return isPali
```


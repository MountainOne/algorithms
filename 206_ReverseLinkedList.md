## LeetCode  206 反转链表
链表
easy

### 描述
反转一个单链表。

### 解答
可以用栈实现。也可以用三个变量，通过一次遍历就实现链表的反转。

```Python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev = None
        while head:
            curr = head
            head = head.next
            curr.next = prev
            prev = curr
        return prev  
```


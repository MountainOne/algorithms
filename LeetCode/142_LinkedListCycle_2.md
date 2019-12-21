## LeetCode  141 环形链表
链表
### 描述
给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。

说明：不允许修改给定的链表。

### 解答
判断链表有环的操作是:
初始化一个快指针一个慢指针，快指针一次走 2 格，慢指针一次走 1 格。当快慢指针相等
时，停止循环。然后让快指针回到初始位置，再次开始移动两个指针，这次两个指针每次都走一格，重合的位置即为
开始循环的位置。

```Python
class Solution:
    def detectCycle(self, head: ListNode) -> ListNode:
        if head == None or head.next == None:
            return None
        slow = head
        fast = head
        is_cycle = False
        while fast != None:
            slow = slow.next
            if fast.next == None : return None
            fast = fast.next.next
            if slow == fast: 
                is_cycle = True
                break
        if not is_cycle: return None
        fast = head
        while fast != slow:
            fast = fast.next
            slow = slow.next
        return fast
```
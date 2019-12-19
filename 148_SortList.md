## LeetCode  148 排序链表
链表 排序
### 描述
在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

### 解答
模拟归并排序对链表进行排序。需要注意的是，在第一次截断链表时，需要多设一个指针，用来保存慢指针
的前一个指针，通过它来截断链表。

```Python
class Solution:
    def sortList(self, head: ListNode) -> ListNode:
        if not head  or not head.next:
            return head
        pre, slow, fast = None, head, head
        while fast and fast.next:
            pre = slow
            slow = slow.next
            fast = fast.next.next
        pre.next = None
        l1 = self.sortList(head)
        l2 = self.sortList(slow)
        return self.merge(l1, l2)
    
    def merge(self, l1, l2):
        head =  nextL = ListNode(None)
        while l1 and l2:
            if l1.val > l2.val:
                nextL.next = l2
                l2 = l2.next               
            else:
                nextL.next = l1
                l1 = l1.next
            nextL = nextL.next
        nextL.next = l1 or l2
        return head.next
```
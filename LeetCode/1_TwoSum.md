## LeetCode  1 两数相加
链表 数学
### 描述
给出两个 非空 的链表用来表示两个非负的整数。其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

示例：
>输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807

### 解答
分别遍历两个链表，将其中的值取出放入各自的栈里，然后再从栈中依次取出值，组成新的数即可。

```Python
class Solution:
    def addTwoNumbers(self, l1, l2):
        """
        :type l1: ListNode
        :type l2: ListNode
        :rtype: ListNode
        """
        stack1 = []
        stack2 = []
        while(l1 != None):
            stack1.append(l1.val)
            l1 = l1.next
        while(l2 != None):
            stack2.append(l2.val)
            l2 = l2.next
        num1 , num2 = 0, 0
        while(len(stack1) != 0):
            num1 = num1 * 10 + stack1.pop()
        while(len(stack2) != 0):
            num2 = num2 * 10 + stack2.pop()
        s = num1 + num2
        root=ListNode(s%10)
        pre=root
        s = s // 10
        while(s != 0):
            cur = ListNode(s%10)
            pre.next=cur
            pre=cur
            s //= 10
        return root
```
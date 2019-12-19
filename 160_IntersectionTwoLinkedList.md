## LeetCode  160 相交链表
链表
easy
### 描述
编写一个程序，找到两个单链表相交的起始节点。

### 解答
这道题的解法很巧妙，关键在于让两个指针都走完两个链表的长度，如果链表相交，那么它们会在相交的那个节点
会合，如果不相交，那么它们就会都走到链表尾，在 None 节点会合。

```Python
class MinStack:

    def __init__(self):
        """
        initialize your data structure here.
        """
        self.stack = []
        self.min_val = float('inf')
        

    def push(self, x: int) -> None:
        self.min_val =  min(x, self.min_val)
        self.stack.append(x)

    def pop(self) -> None:
        tmp = self.stack.pop()
        if tmp == self.min_val:
            self.min_val = float('inf')
            for i in range(len(self.stack)):
                self.min_val = min(self.min_val, self.stack[i])

    def top(self) -> int:
        length = len(self.stack)
        return self.stack[length - 1]

    def getMin(self) -> int:
        return self.min_val
```
## LeetCode  155 最小栈
栈 设计
easy
### 描述
设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。

### 解答
在传统的栈的基础上，增加一个变量`min_val`记录最小值，每次插入时，和`min_val`比较，如果更小就更新最小值。每次`pop()`时，如果出栈的是`min_val`，则遍历栈，重新选出`min_val`。

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
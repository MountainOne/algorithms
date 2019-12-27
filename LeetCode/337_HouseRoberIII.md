## LeetCode  337  打家劫舍 III
- 树 
- medium

### 描述
在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。

示例 1:

输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1

输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
示例 2:

输入: [3,4,5,1,3,null,1]

     3
    / \
   4   5
  / \   \ 
 1   3   1

输出: 9
解释: 小偷一晚能够盗取的最高金额 = 4 + 5 = 9.

### 解答
递归遍历二叉树，返回两个变量。一个是当前节点被打劫，另一个是当前节点没被打劫。当前节点被打劫时，
该值等于` now = node.val + left[1] + right[1]`，该节点没被打劫时，该值等于` after = max(left) + max(right)`。


```Python
class Solution:
    def rob(self, root: TreeNode) -> int:
        def superrob(node):
            if not node: return (0, 0)
            left, right = superrob(node.left), superrob(node.right)
            now = node.val + left[1] + right[1]
            after = max(left) + max(right)
            return (now, after)
        return max(superrob(root))
```


## LeetCode  236 二叉树的最近公共祖先
- 树
- easy

### 描述
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]


### 解答
解答树相关的题首先考虑递归。本题中，递归结束的情况时当前节点为空，或者为两个目标节点的一个。
在中间状态的情况是，如果包含其中一个节点，则返回该节点，如果都不包含，则返回空，如果都包含，则返回自己。

```Python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        if root in (None, p, q):
            return root
        left, right = [ self.lowestCommonAncestor(node, p, q)\
                       for node in (root.left, root.right)]
        return root if left and right else left or right
```


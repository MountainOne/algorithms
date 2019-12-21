## LeetCode  226 翻转二叉树
- 树
- easy

### 描述
翻转一棵二叉树。


### 解答
将左右子树颠倒即可。

```Python
class Solution:
    def invertTree(self, root: TreeNode) -> TreeNode:
        if not root: return None
        if root.left: 
            root.left = self.invertTree(root.left)
        if root.right:
            root.right = self.invertTree(root.right)
        root.left, root.right = root.right, root.left
        return root
```


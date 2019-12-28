## LeetCode  543  二叉树的直径
- 树
- easy

### 描述
给定一棵二叉树，你需要计算它的直径长度。一棵二叉树的直径长度是任意两个结点路径长度中的最大值。这条路径可能穿过根结点。

示例 :
给定二叉树

          1
         / \
        2   3
       / \     
      4   5    
返回 3, 它的长度是路径 [4,2,1,3] 或者 [5,2,1,3]。

注意：两结点之间的路径长度是以它们之间边的数目表示。

### 解答
每个节点返回左子节点和右子节点中的较大值加 1，当节点为空时返回 0.


```Python
class Solution:
    D = 0
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        if not root: return 0
        self.traverse(root)
        return self.D - 1
        
    def traverse(self, node):
        if not node:
            return 0
        left = self.traverse(node.left)
        right = self.traverse(node.right)
        self.D = max(left + right + 1, self.D)
        return max(left, right) + 1
```


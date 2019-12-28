## LeetCode  617  合并二叉树
- 树
- easy

### 描述
给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。

示例 1:

输入: 
	Tree 1                     Tree 2                  
          1                         2                             
         / \                       / \                            
        3   2                     1   3                        
       /                           \   \                      
      5                             4   7                  
输出: 
合并后的树:
	     3
	    / \
	   4   5
	  / \   \ 
	 5   4   7
注意: 合并必须从两个树的根节点开始。

### 解答
前序遍历，产生的新节点的值为两棵树对应节点值之和。若某棵树的节点值为空，则返回另一棵树的节点。如果
都为空，则返回 None。

```Python
class Solution:
    def mergeTrees(self, t1: TreeNode, t2: TreeNode) -> TreeNode:
        if not t1 or not t2: return t1 or t2
        return self.merge(t1, t2)
        
    def merge(self, t1, t2):
        if not t1 and not t2:
            return None
        elif not t1 or not t2:
            return t1 or t2
        cur = ListNode(t1.val + t2.val)
        cur.left = self.merge(t1.left, t2.left)
        cur.right = self.merge(t1.right, t2.right)
        return cur          
```


## 101. Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).
>For example, this binary tree [1,2,2,3,4,4,3] is symmetric:
   >1
   / \
  2   2
 / \ / \
3  4 4  3
 

> But the following [1,2,2,null,3,null,3] is not:
   1
   / \
  2   2
   \   \
   3    3

递归：
```
class Solution:
    def isMirror(self, t1: TreeNode, t2: TreeNode) -> bool:
        if (t1 == None and t2 == None): return True
        if (t1 == None or t2 == None): return False

        return (t1.val == t2.val
        and self.isMirror(t1.right, t2.left)
        and self.isMirror(t1.left, t2.right))
        
    def isSymmetric(self, root: TreeNode) -> bool:
        return self.isMirror(root, root)
```

迭代：
```

```


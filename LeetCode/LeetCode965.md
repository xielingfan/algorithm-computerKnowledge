```python
# 如果二叉树每个节点都具有相同的值，那么该二叉树就是单值二叉树。 
# 
#  只有给定的树是单值二叉树时，才返回 true；否则返回 false。 
# 
#  
# 
#  示例 1： 
# 
#  
# 
#  输入：[1,1,1,1,1,null,1]
# 输出：true
#  
# 
#  示例 2： 
# 
#  
# 
#  输入：[2,2,2,5,2]
# 输出：false
#  
# 
#  
# 
#  提示： 
# 
#  
#  给定树的节点数范围是 [1, 100]。 
#  每个节点的值都是整数，范围为 [0, 99] 。 
#  
#  Related Topics 树 
#  👍 62 👎 0


#Python3
#执行耗时:40 ms,击败了76.76% 的Python3用户
#内存消耗:13.4 MB,击败了20.26% 的Python3用户
# leetcode submit region begin(Prohibit modification and deletion)
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def isUnivalTree(self, root: TreeNode) -> bool:
        val = root.val

        def dfs(node):
            if not node: return True
            if node:
                if (node.val != val):
                    return False
                return dfs(node.left) and dfs(node.right)

        return dfs(root)
# leetcode submit region end(Prohibit modification and deletion)
```


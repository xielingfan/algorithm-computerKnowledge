#### [107. 二叉树的层次遍历 II](https://leetcode-cn.com/problems/binary-tree-level-order-traversal-ii/)



# 题目描述

给定一个二叉树，返回其节点值自底向上的层次遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

# 示例

```
例如：
给定二叉树 [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其自底向上的层次遍历为：

[
  [15,7],
  [9,20],
  [3]
]

```
# 代码

```java
//java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        Deque<TreeNode> queue = new LinkedList<>();
        if(root == null) return res;
        queue.offerLast(root);
        while (!queue.isEmpty()){
            List<Integer> level = new LinkedList<>();

            int curLevelSize = queue.size();
            for(int i = 0; i < curLevelSize; ++i){
                TreeNode node = queue.pollFirst();
                level.add(node.val);
                if(node.left != null) queue.offerLast(node.left);
                if(node.right != null) queue.offerLast(node.right);
            }
            res.add(0,level);
        }
        return res;
    }
}
```

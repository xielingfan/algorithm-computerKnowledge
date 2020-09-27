#### [110. 平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

# 题目描述
```
给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过1。

示例 1:

给定二叉树 [3,9,20,null,null,15,7]

    3
   / \
  9  20
    /  \
   15   7
返回 true 。

示例 2:

给定二叉树 [1,2,2,3,3,null,null,4,4]

       1
      / \
     2   2
    / \
   3   3
  / \
 4   4
返回 false 。

```

# 代码

```java
//自顶向下递归
//对于同一个节点，depth函数会被重复调用，时间复杂度较高
class Solution {
    public boolean isBalanced(TreeNode root) {
        if(root == null) return true;
        if(Math.abs(depth(root.left)-depth(root.right)) > 1) return false;
        return isBalanced(root.left) && isBalanced(root.right);
    }

    private int depth(TreeNode root){
        if(root == null) return 0;
        return Math.max( depth(root.left) ,depth(root.right) ) + 1;
    }
}
```

```java
//自底向上的递归
//自底向上递归的做法类似于后序遍历，对于当前遍历到的节点，先递归地判断其左右子树是否平衡，再判断以当前节点为根的子树是否平衡。
//如果一棵子树是平衡的，则返回其高度（高度一定是非负整数），否则返回 -1。
//如果存在一棵子树不平衡，则整个二叉树一定不平衡。

class Solution {
    public boolean isBalanced(TreeNode root) {
        return depth(root) >= 0;
    }

    private int depth(TreeNode root){
        if(root == null) return 0;
        int ld = depth(root.left);
        int rd = depth(root.right);
        if(ld == -1 || rd == -1 || Math.abs(ld - rd) > 1) return -1;
        else return Math.max(ld,rd) + 1;
    }
}
```
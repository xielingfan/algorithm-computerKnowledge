#### [144. 二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)

# 题目描述

给定一个二叉树，返回它的 前序 遍历。

进阶: 递归算法很简单，你可以通过迭代算法完成吗？

**示例：**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,2,3]
```

# 代码

```java
//java
//递归
class Solution {
    ArrayList<Integer> res = new ArrayList<>();
    public List<Integer> preorderTraversal(TreeNode root) {
        if(root != null){
            res.add(root.val);
            preorderTraversal(root.left);
            preorderTraversal(root.right);
        }
        return res;
    }
}
```

```java
//java
//栈
//先访问根节点
//根据栈的先入后出性质，先将右孩子压栈，再将左孩子压栈
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        LinkedList<TreeNode> stack = new LinkedList<>();
        LinkedList<Integer> res = new LinkedList<>();

        if(root == null) return res;
        stack.add(root);
        while (!stack.isEmpty()){
            TreeNode tmp = stack.pollLast();
            res.add(tmp.val);
            if(tmp.right != null) stack.add(tmp.right);
            if(tmp.left != null) stack.add(tmp.left);
        }
        return res;
    }
}
```

```java
//java
//莫里斯遍历
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        LinkedList<Integer> res = new LinkedList<>();

        TreeNode cur = root;
        while(cur != null){
            if(cur.left == null) {
                res.add(cur.val);
                cur = cur.right;
            }else {
                TreeNode pre = cur.left;
                while ((pre.right != null) && (pre.right != cur)){
                    pre = pre.right;
                }

                if(pre.right == null){  //第一次到达左子树最右端
                    res.add(cur.val);
                    pre.right = cur;
                    cur = cur.left;
                }else {                 //第二次到达左子树最右端
                    pre.right = null;
                    cur = cur.right;
                }
            }
        }
        return res;
    }
}
```
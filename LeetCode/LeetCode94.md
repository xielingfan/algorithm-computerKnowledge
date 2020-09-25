#### [94. 二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)

# 题目描述

给定一个二叉树，返回它的 *中序* 遍历。

进阶: 递归算法很简单，你可以通过迭代算法完成吗？

**示例：**

```
输入: [1,null,2,3]  
   1
    \
     2
    /
   3 

输出: [1,3,2]
```

# 代码

```java
//java
//递归
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        inorder(root, res);
        return res;
    }

    public void inorder(TreeNode root, List<Integer> res) {
        if (root == null) return;
        inorder(root.left, res);
        res.add(root.val);
        inorder(root.right, res);
    }
}
```

```java
//java
//栈
//因为遍历顺序是左-根-右，所以先把根压栈，一路向左访问，一路压栈
//直到找到最左节点，输出后访问右孩子，没有则从栈中取一个节点
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        Deque<TreeNode> stk = new LinkedList<TreeNode>();
        while (root != null || !stk.isEmpty()) {
            while (root != null){
                stk.push(root);
                root = root.left;
            }
            root = stk.pop();
            res.add(root.val);
            root = root.right;
        }
        return res;
    }
}
```

```java
//java
//莫里斯遍历
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        LinkedList<Integer> res = new LinkedList<>();

        TreeNode cur = root;
        while(cur != null){
            if(cur.left == null) {   //没有左子树
                res.add(cur.val);
                cur = cur.right;
            }else {
                TreeNode pre = cur.left;
                while ((pre.right != null) && (pre.right != cur)){      //找左子树的最右节点
                    pre = pre.right;
                }

                if(pre.right == null){  //第一次到达左子树最右端
                    pre.right = cur;
                    cur = cur.left;
                }else {                 //第二次到达左子树最右端
                    pre.right = null;
                    res.add(cur.val);   //左子树都整完了，输出根节点，然后转向右子树
                    cur = cur.right;
                }
            }
        }
        return res;
    }
}
```
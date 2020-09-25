#### [145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

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

输出: [3,2,1]
```

# 代码

```java
//java
//递归
class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        postorder(root,res);
        return res;
    }

    private void postorder(TreeNode root , List<Integer> res){
        if(root == null) return;
        postorder(root.left , res);
        postorder(root.right , res);
        res.add(root.val);
    }
}
```

```java
//java
//栈
//当遍历完某个根节点的左子树，回到根节点的时候，对于中序遍历和先序遍历可以把当前根节点从栈里弹出，然后转到右子树
//而对于后序遍历，当我们到达某个根节点的时候并不能立刻把它弹出，因为遍历完右子树，我们还需要将这个根节点加入到 res 中。
//所以我们就需要判断是从左子树到的根节点，还是右子树到的根节点。
//如果是从左子树到的根节点，此时应该转到右子树。如果是从右子树到的根节点，那么就可以把当前节点弹出，并且加入到 res 中。
//如果是从左子树到的根节点，此时如果根节点的右子树为 null， 此时也可以把当前节点弹出，并且加入到 list 中。

class Solution {
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> res = new LinkedList<>();
        Deque<TreeNode> stk = new LinkedList<>();

        TreeNode cur = root;
        TreeNode pre = null;
		//通过记录上一次遍历的节点。如果当前节点的右节点和上一次遍历的节点相同，那就表明当前是从右节点过来的了。
        while(cur != null || !stk.isEmpty()){
            while (cur != null) {
                stk.push(cur);
                cur = cur.left;
            }
            TreeNode tmp = stk.peek();
            if(tmp.right != null && tmp.right != pre){
                cur = tmp.right;
            }else{
                res.add(tmp.val);
                pre = tmp;
                stk.pop();
            }
        }
        return res;
    }
}
```
[617. 合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)

# 题目描述

给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。

# 示例

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

# 题解

可以对两棵树进行先序遍历，并直接对t1进行修改，如果t1和t2都不为空，就可以继续递归，否则如果两个都为空，就返回null，否则，返回非空的。

# 代码

```c++
//c++
//执行用时：72 ms, 在所有 C++ 提交中击败了80.93%的用户
//内存消耗：32.2 MB, 在所有 C++ 提交中击败了90.70%的用户

class Solution {
public:
    TreeNode* mergeTrees(TreeNode* t1, TreeNode* t2) {
        TreeNode *root=t1;
        if(t1&&t2){
            root->val+=t2->val;
            root->left=mergeTrees(t1->left,t2->left);
            root->right=mergeTrees(t1->right,t2->right);
        }
        else if(!t1&&t2)
            return t2;
        else if(t1&&!t2) 
            return t1;
        //两个都不存在
        else return NULL;
        return root;
    }
};

//java
class Solution {
    public TreeNode mergeTrees(TreeNode t1, TreeNode t2) {
        if(t1 == null && t2 == null) {
            return null;
        }
        if(t1 == null) {
            return t2;
        }
        if(t2 == null) {
            return t1;
        }
        TreeNode merged = new TreeNode(t1.val + t2.val);
        merged.left = mergeTrees(t1.left, t2.left);
        merged.right = mergeTrees(t1.right, t2.right);
        return merged;
    }
}
```

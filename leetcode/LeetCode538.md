#### [538. 把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

# 题目描述

给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)，使得每个节点的值是原来的节点值加上所有大于它的节点值之和。

# 示例

输入: 原始二叉搜索树:
              5
            /   \
           2     13

输出: 转换为累加树:
             18
            /   \
          20     13

# 题解

用反向的中序遍历来解题，pre表示之前节点的值，初始为0。

# 代码

```C++
//c++
//运行时间：68ms
//运行内存：32.5MB

class Solution {
public:
    void convertBST(TreeNode *&root,int &pre){
        if(!root) return;
        convertBST(root->right,pre);
        root->val+=pre;
        pre=root->val;
        convertBST(root->left,pre);
    }
    TreeNode* convertBST(TreeNode* root) {
        int pre=0;
        convertBST(root,pre);
        return root;
    }
};
```


#### [114. 二叉树展开为链表](https://leetcode-cn.com/problems/flatten-binary-tree-to-linked-list/)

# 题目描述

给定一个二叉树，[原地](https://baike.baidu.com/item/原地算法/8010757)将它展开为一个单链表。

# 示例

```
    1
   / \
  2   5
 / \   \
3   4   6
```

转为：

```
1
 \
  2
   \
    3
     \
      4
       \
        5
         \
          6
```



# 代码

```c++
class Solution {
public:
    void flatten(TreeNode* root) {
        if(!root)return;
        //后序遍历
        flatten(root->left);
        flatten(root->right);
        if(root->left){
            auto pre=root->left;
            while(pre->right)
                pre=pre->right;
            pre->right=root->right;
            root->right=root->left;
            root->left=nullptr;
        }
        root=root->right;
        return;
    }
};
```


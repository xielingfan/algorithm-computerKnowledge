#### [337. 打家劫舍 III](https://leetcode-cn.com/problems/house-robber-iii/)



# 题目描述

在上次打劫完一条街道之后和一圈房屋后，小偷又发现了一个新的可行窃的地区。这个地区只有一个入口，我们称之为“根”。 除了“根”之外，每栋房子有且只有一个“父“房子与之相连。一番侦察之后，聪明的小偷意识到“这个地方的所有房屋的排列类似于一棵二叉树”。 如果两个直接相连的房子在同一天晚上被打劫，房屋将自动报警。

计算在不触动警报的情况下，小偷一晚能够盗取的最高金额。



# 示例

```
输入: [3,2,3,null,3,null,1]

     3
    / \
   2   3
    \   \ 
     3   1
输出: 7 
解释: 小偷一晚能够盗取的最高金额 = 3 + 3 + 1 = 7.
```



# 题解

对于每一个节点root来说，有选或者不选两种可能，用unordered_map f来表示如果选择root盗取的最大金额，g来表示不选root盗取的最大金额,采用后续遍历的方法。



# 代码

```c++
//c++
//执行用时：48 ms, 在所有 C++ 提交中击败了26.92%的用户
//内存消耗：28.9 MB, 在所有 C++ 提交中击败了22.53%的用户

class Solution {
public:
    unordered_map<TreeNode*,int> f,g;
    void dfs(TreeNode *root){
        if(!root) return;
        dfs(root->left);
        dfs(root->right);
        //f表示选择root的最大值，g表示不选root的最大值
        f[root]=g[root->left]+g[root->right]+root->val;
        g[root]=max(f[root->left],g[root->left])+max(f[root->right],g[root->right]);
    }
    int rob(TreeNode* root) {
        dfs(root);
        return max(f[root],g[root]);
    }
};
```


# 参与规范

## LeetCode题解

题解放在Leetcode文件夹中
题解需要包含leetcode题目链接
题解命名规则：LeetCode27.md

### 题解示例（代码上方说明自己使用什么语言）
题目链接：https://leetcode-cn.com/problems/sum-of-left-leaves/

```c++
//C++
//使用深度优先搜索遍历所有节点，在传入参数时使用不同变量标记该节点是左孩子还是右孩子，当且仅当一个节点同时满足叶子结点和左孩子将该节点的值累加到结果上
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    int sumOfLeftLeaves(TreeNode* root) {
        if(root == NULL) return 0;
        int res = 0; //存储结果
        dfs(root, -1, res);
        return res;
    }
    //使用flag标记当前节点的性质，-1为根节点，0为左子树，1为右子树
    void dfs(TreeNode* root, int flag, int& res) {
        if(root == NULL) return;
        if(root->left == NULL && root->right == NULL && flag == 0) {
            res += root->val; //当前节点为叶子节点且标记为左孩子时才累加结果
        }
        dfs(root->left, 0, res); //遍历左子树
        dfs(root->right, 1, res); //遍历右子树
    }
};
```





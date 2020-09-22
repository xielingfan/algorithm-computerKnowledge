#### [968. 监控二叉树](https://leetcode-cn.com/problems/binary-tree-cameras/)

# 题目描述

给定一个二叉树，我们在树的节点上安装摄像头。

节点上的每个摄影头都可以监视**其父对象、自身及其直接子对象。**

计算监控树的所有节点所需的最小摄像头数量。

 # 示例

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/12/29/bst_cameras_01.png)

```
输入：[0,0,null,0,0]
输出：1
解释：如图所示，一台摄像头足以监控所有节点。
```

# 题解

所有节点都有以下三种状态：

1. 等待被摄像头监控，不妨设为状态0
2. 已被监控，不妨设为状态1
3. 安装了摄像头，不妨设为状态2

然后进行dfs

# 代码

```c++
//c++
//运行时间：12ms，在所有 C++ 提交中击败了93.21%的用户
//运行内存：20.8MB，在所有 C++ 提交中击败了39.19%的用户
class Solution {
public:
    //0: 待监控
    //1：已被监控
    //2：已安装摄像头
    int dfs(TreeNode *root,int &ans){
        //如果root为空，可以理解为已经覆盖
        if(!root)
            return 1;
        //后序遍历
        int left=dfs(root->left,ans);
        int right=dfs(root->right,ans);
        //只要两个孩子需要被监控，就在当前节点安装摄像头
        if(left==0||right==0){
            ans++;
            return 2;
        }
        //如果两个孩子有一个被监控，当前节点设为待监控
        if(left==1&&right==1)
            return 0;
        //如果两个孩子一个有摄像头2，一个被监控1，那么当前节点就被监控1（如果只是一个孩子有摄像头2，而另一个待监控0，那么当前节点不能被设为已被监控1）
        if(left+right>2)
            return 1;
        return -1;

    }
    int minCameraCover(TreeNode* root) {
        int ans=0;
        //如果根节点待监控，说明此节点必须放置摄像头
        if(dfs(root,ans)==0){
            ++ans;
        }
        return ans;
    }
};
```


#### [106. 从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)



# 题目描述

根据一棵树的中序遍历与后序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。



# 示例

```
中序遍历 inorder = [9,3,15,20,7]
后序遍历 postorder = [9,15,7,20,3]
```

```
 输出：
 	3
   / \
  9  20
    /  \
   15   7
```



# 代码

```c++
//c++
//执行用时：24 ms, 在所有 C++ 提交中击败了77.37%的用户
//内存消耗：17.1 MB, 在所有 C++ 提交中击败了62.42%的用户

class Solution {
public:
    TreeNode* buildTree(vector<int> &In,vector<int> &Post,int inL,int inR,int postL,int postR){
        if(inL>inR)return NULL;
        TreeNode *root=new TreeNode(Post[postR]);
        //计算左子树的节点数
        int k;
        for(k=inL;k<=inR;++k){
            if(In[k]==root->val)
                break;
        }
        //leftnum表示左子树的节点数
        int leftnum=k-inL;
        root->left=buildTree(In,Post,inL,inL+leftnum-1,postL,postL+leftnum-1);
        root->right=buildTree(In,Post,k+1,inR,postL+leftnum,postR-1);
        return root;
    }
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        return buildTree(inorder,postorder,0,inorder.size()-1,0,postorder.size()-1);
    }
};
```

```java
//java
//执行耗时:2 ms,击败了97.53% 的Java用户
//内存消耗:39.2 MB,击败了52.91% 的Java用户
class Solution {

    int post_idx;
    int[] postorder;
    int[] inorder;
    Map<Integer,Integer> idx_map = new HashMap<>();

    public TreeNode helper(int in_left, int in_right) {
        if(in_left > in_right){
            return null;
        }

        int root_val = postorder[post_idx];
        TreeNode root = new TreeNode(root_val);

        int index = idx_map.get(root_val);

        --post_idx;
        root.right = helper(index+1,in_right);
        root.left = helper(in_left, index - 1);
        return root;
    }

    public TreeNode buildTree(int[] inorder, int[] postorder) {
        this.postorder = postorder;
        this.inorder = inorder;
        post_idx = postorder.length - 1;

        int idx = 0;
        for (Integer val : inorder){
            idx_map.put(val,idx++);
        }

        return helper(0,inorder.length-1);
    }
}
```


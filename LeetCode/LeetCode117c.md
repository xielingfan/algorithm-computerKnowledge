#### [117. 填充每个节点的下一个右侧节点指针II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)

# 题目描述
```
给定一个二叉树

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。


进阶：

你只能使用常量级额外空间。
使用递归解题也符合要求，本题中递归程序占用的栈空间不算做额外的空间复杂度。

示例：
https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2019/02/15/117_sample.png

输入：root = [1,2,3,4,5,null,7]
输出：[1,#,2,3,#,4,5,7,#]
解释：给定二叉树如图 A 所示，你的函数应该填充它的每个 next 指针，以指向其下一个右侧节点，如图 B 所示。
 

提示：

树中的节点数小于 6000
-100 <= node.val <= 100


```

# 代码

```c++
//执行耗时:12 ms,击败了99.05% 的C++用户
//内存消耗:17.1 MB,击败了72.75% 的C++用户
class Solution {
public:
    Node* connect(Node* root) {
        if(root==NULL || (root->left==NULL && root->right==NULL)) return root; 
        //root->next=NULL;
        if(root->left!=NULL){
            if(root->right!=NULL){
                root->left->next=root->right;
                root->right->next=findNext(root->next);
            }
            else{
                root->left->next=findNext(root->next);
            }
        }
        else{
            root->right->next=findNext(root->next);
        }
        connect(root->right);
        connect(root->left);
        return root;
    }
    Node* findNext(Node* root){
        if(root==NULL) return NULL;
        else{
            if(root->left!=NULL||root->right!=NULL){
                if(root->left!=NULL)
                    return root->left;
                else 
                    return root->right;
            }
            else
                return findNext(root->next);
        }
    }
};
```

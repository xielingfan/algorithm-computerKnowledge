#### [102. 二叉树的层序遍历](https://leetcode-cn.com/problems/binary-tree-level-order-traversal/)

# 题目描述
```
给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

示例：
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]

```

# 代码

```java
//执行耗时:1 ms,击败了92.92% 的Java用户
//内存消耗:39.1 MB,击败了38.27% 的Java用户
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList<List<Integer>>();
        Deque<TreeNode> queue = new LinkedList<>();
        if(root == null) return res;
        queue.offerLast(root);
        while (!queue.isEmpty()){
            List<Integer> level = new LinkedList<>();

            int curLevelSize = queue.size();
            for(int i = 0; i < curLevelSize; ++i){
                TreeNode node = queue.pollFirst();
                level.add(node.val);
                if(node.left != null) queue.offerLast(node.left);
                if(node.right != null) queue.offerLast(node.right);
            }
            res.add(level);
        }
        return res;
    }
}
```
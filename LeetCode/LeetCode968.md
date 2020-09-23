#### [968.监控二叉树](https://leetcode-cn.com/problems/binary-tree-cameras/)

# 题目描述

给定一个二叉树，我们在树的节点上安装摄像头。

节点上的每个摄影头都可以监视其父对象、自身及其直接子对象。

计算监控树的所有节点所需的最小摄像头数量。

# 题解

```java
/**
 * 三种状态
 * 0: 未覆盖
 * 1：已覆盖（本节点未安装摄像头）
 * 2：已安装摄像头
 */
```

# 代码

```java
class Solution {
    int res = 0;

    public int minCameraCover(TreeNode root) {
        if(lrd(root) == 0){
            ++res;
        }
        return res;
    }

    private int lrd(TreeNode node){
        if(node == null) return 1;

        int left = lrd(node.left);
        int right = lrd(node.right);

        //左右孩子有一个未被覆盖，则在该节点装摄像头，状态为2
        if(left == 0 || right == 0){
            ++res;
            return 2;
        }
        //左右孩子都被覆盖，则不在该节点装摄像头，状态为0
        if(left == 1 && right == 1){
            return 0;
        }
        //左右孩子都被覆盖，并且至少一个孩子安装了摄像头，则该节点已覆盖，状态为1
        if(left + right >= 3){
            return 1;
        }

        return -1;

    }
}
```

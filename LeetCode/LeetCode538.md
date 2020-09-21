```java
//给定一个二叉搜索树（Binary Search Tree），把它转换成为累加树（Greater Tree)，使得每个节点的值是原来的节点值加上所有大于它的节
//点值之和。 
//
// 
//
// 例如： 
//
// 输入: 原始二叉搜索树:
//              5
//            /   \
//           2     13
//
//输出: 转换为累加树:
//             18
//            /   \
//          20     13
// 
//
// 
//
// 注意：本题和 1038: https://leetcode-cn.com/problems/binary-search-tree-to-greater-s
//um-tree/ 相同 
// Related Topics 树 
// 👍 345 👎 0


//java
//执行耗时:1 ms,击败了97.82% 的Java用户
//内存消耗:39.2 MB,击败了22.86% 的Java用户
//通过右根左的遍历方式从最大的节点开始遍历，然后累加这些节点的值替换节点本来的值。
//leetcode submit region begin(Prohibit modification and deletion)
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    int sum = 0; //使用全局变量保存累加值
    public TreeNode convertBST(TreeNode root) {
        if(root == null) return null;
        convertBST(root.right); //遍历右子树
        sum += root.val; //累加值
        root.val = sum; //改变当前节点的值
        convertBST(root.left); //遍历左子树
        return root;
    }
}
//leetcode submit region end(Prohibit modification and deletion)
```
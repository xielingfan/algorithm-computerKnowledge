#### [501. 二叉搜索树中的众数](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/)

# 题目描述

给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

结点左子树中所含结点的值小于等于当前结点的值
结点右子树中所含结点的值大于等于当前结点的值
左子树和右子树都是二叉搜索树
例如：
给定 BST [1,null,2,2],

   1
    \
     2
    /
   2
返回[2].


# 代码

```java
//java
//执行耗时:0 ms,击败了100.00% 的Java用户
//内存消耗:39.3 MB,击败了70.02% 的Java用户
//利用二叉搜索树的性质，中序遍历是一个非递减序列，相同元素是连续的
//用basebase 记录当前的数字，用countcount 记录当前数字重复的次数，用maxCountmaxCount 来维护已经扫描过的数当中出现最多的那个数字的出现次数，用 answeranswer 数组记录出现的众数

class Solution {
    int base,count,maxCount;
    List<Integer> ans = new ArrayList<>();
    public int[] findMode(TreeNode root) {
        inorder(root);
        int[] res = new int[ans.size()];
        for(int i = 0; i < ans.size(); ++i){
            res[i] = ans.get(i);
        }
        return res;
    }
    public void inorder(TreeNode root) {
        if (root == null) return;
        inorder(root.left);
        uptate(root.val);
        inorder(root.right);
    }
    public void uptate(int x){
        if(x != base){
            base = x;
            count = 1;
        }else {
            ++count;
        }
        if(count == maxCount){
            ans.add(base);
        }
        if(count > maxCount){
            maxCount = count;
            ans.clear();
            ans.add(base);
        }
    }
}
```

```java
//java
//执行耗时:0 ms,击败了100.00% 的Java用户
//内存消耗:39.5 MB,击败了56.78% 的Java用户
class Solution {
    List<Integer> ans = new ArrayList<Integer>();
    int nownum, nowcount = 0, maxcount = 0;
    public void dfs(TreeNode root) {
        if(root == null) return;
        if(root.left != null) {
            dfs(root.left);
        }
        if(root.val == nownum) {
            nowcount++;
        } else {
            nowcount = 1;
            nownum = root.val;
        }
        if(nowcount > maxcount) {
            maxcount = nowcount;
            ans.clear();
            ans.add(root.val);
        } else if(nowcount == maxcount) {
            ans.add(root.val);
        }
        if(root.right != null) {
            dfs(root.right);
        }
    }
    public int[] findMode(TreeNode root) {
        dfs(root);
        int[] res = new int[ans.size()];
        for(int i = 0; i < ans.size(); ++i) {
            res[i] = ans.get(i);
        }
        return res;
    }
}
```


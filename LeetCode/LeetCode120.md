#### [120. 三角形最小路径和](https://leetcode-cn.com/problems/triangle/)

# 题目描述

给定一个三角形，找出自顶向下的最小路径和。每一步只能移动到下一行中相邻的结点上。

相邻的结点 在这里指的是 下标 与 上一层结点下标 相同或者等于 上一层结点下标 + 1 的两个结点。

# 示例

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
```

自顶向下的最小路径和为 `11`（即，**2** + **3** + **5** + **1** = 11）。



# 题解

采用动态规划的解法，初始状态为:dp\[n-1][i]=triangle\[n-1][i],0<i<n

状态转移方程为：dp\[i][j]=triangle\[i][j]+min(dp\[i+1][j],dp\[i+1][j+1])

# 代码

```c++
//c++
//执行用时：4 ms,在所有 C++ 提交中击败了99.81%的用户
//内存消耗：8.3 MB, 在所有 C++ 提交中击败了41.13%的用户

class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        int n=triangle.size();
        vector<vector<int>> dp(n,vector<int>(n));
        //初始状态，最后一行的dp值就是本身的值
        for(int i=0;i<n;++i)
            dp[n-1][i]=triangle[n-1][i];
        //从倒数第二行开始向第一行遍历
        for(int i=n-2;i>=0;--i)
            for(int j=0;j<=i;++j){
                dp[i][j]=triangle[i][j]+min(dp[i+1][j],dp[i+1][j+1]);
            }
        return dp[0][0];
    }
};
```


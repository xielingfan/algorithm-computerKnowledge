#### [64. 最小路径和](https://leetcode-cn.com/problems/minimum-path-sum/)

# 题目描述

给定一个包含非负整数的 *m* x *n* 网格，请找出一条从左上角到右下角的路径，使得路径上的数字总和为最小。

**说明：**每次只能向下或者向右移动一步。



# 示例

```
输入:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
输出: 7
解释: 因为路径 1→3→1→1→1 的总和最小。
```



# 题解

本题采用动态规划的方法，设置dp\[i][j]表示从左上角的点出发到点(i,j)路径上最小的和，由于题目规定每次只能向下或者向右移动一步，所以dp\[i][j]就只与它上面和它左面的dp有关

状态转移方程为：dp\[i][j]=grid\[i-1][j-1]+min(dp\[i-1][j],dp\[i][j-1]),在这里，dp数组是在最外层加了一边，所以dp\[i][j]对应的点为grid\[i-1][j-1]

初始状态为dp\[i][0]=inf,0<i<=m,dp\[0][j]=inf,0<j<=n



# 代码

```c++
//c++
//执行用时：24 ms, 在所有 C++ 提交中击败了9.64%的用户
//内存消耗：10.1 MB, 在所有 C++ 提交中击败了5.01%的用户

class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m=grid.size();
        int n=grid[0].size();
        vector<vector<int>> dp(m+1,vector<int>(n+1,0));
        int inf=0xff;
        for(int j=0;j<=n;++j)
            dp[0][j]=inf;
        for(int i=0;i<=m;++i)
            dp[i][0]=inf;
        for(int i=1;i<=m;++i)
            for(int j=1;j<=n;++j){
                if(i==1&&j==1)
                    dp[i][j]=grid[i-1][j-1];
                else
                    dp[i][j]=grid[i-1][j-1]+min(dp[i-1][j],dp[i][j-1]);
            }
        return dp[m][n];
    }
};
```






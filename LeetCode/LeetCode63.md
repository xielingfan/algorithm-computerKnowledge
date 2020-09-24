#### [63. 不同路径 II](https://leetcode-cn.com/problems/unique-paths-ii/)



# 题目描述

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

现在考虑网格中有障碍物。那么从左上角到右下角将会有多少条不同的路径？

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)



# 示例

```
输入:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
输出: 2
```



# 题解

本题在[62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)的基础上增加了条件：设置了障碍，那么只需在之前的思想上加一个条件就可以了，如果obstacleGrid\[i][j]是障碍，那么设置dp\[i][j]=0,就可以了，其他不变



# 代码

```c++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m=obstacleGrid.size();
        if(m<=0)
            return 0;
        int n=obstacleGrid[0].size();
        vector<vector<int>> dp(m,vector<int>(n,1));
        for(int i=0;i<m;++i)
            for(int j=0;j<n;++j){
                //如果当前节点是障碍
                if(obstacleGrid[i][j]==1)
                    dp[i][j]=0;
                else{
                    if(i==0&&j==0)
                        dp[i][j]=1;
                    else if(i==0)
                        dp[i][j]=dp[i][j-1];
                    else if(j==0)
                        dp[i][j]=dp[i-1][j];
                    //i和j都不为0
                    else
                        dp[i][j]=dp[i-1][j]+dp[i][j-1];
                }
            }
        return dp[m-1][n-1];
    }
};
```






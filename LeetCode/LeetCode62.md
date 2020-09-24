#### [62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)



 # 题目描述

一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。

机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2018/10/22/robot_maze.png)

# 示例

```
输入: m = 3, n = 2
输出: 3
```

```
输入: m = 7, n = 3
输出: 28
```



# 题解

采用动态规划的解法

初始状态：dp\[i][0]=1,0<=i<m,dp\[0][j]=1,0<=j<n

状态转移方程：dp\[i][j]=dp\[i-1][j]+dp\[i][j-1]



# 代码

```c++
class Solution {
public:
    int uniquePaths(int m, int n) {
    	//初始化
        vector<vector<int>> dp(m,vector<int>(n,1));
        for(int i=1;i<m;++i)
            for(int j=1;j<n;++j)
                dp[i][j]=dp[i-1][j]+dp[i][j-1];
        return dp[m-1][n-1];
    }
};
```


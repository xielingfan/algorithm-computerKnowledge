#### [486. 预测赢家](https://leetcode-cn.com/problems/predict-the-winner/)

# 题目描述

给定一个表示分数的非负整数数组。 玩家 1 从数组任意一端拿取一个分数，随后玩家 2 继续从剩余数组任意一端拿取分数，然后玩家 1 拿，…… 。每次一个玩家只能拿取一个分数，分数被拿取之后不再可取。直到没有剩余分数可取时游戏结束。最终获得分数总和最多的玩家获胜。

给定一个表示分数的数组，预测玩家1是否会成为赢家。你可以假设每个玩家的玩法都会使他的分数最大化。

# 示例

```
输入：[1, 5, 2]
输出：False
```

# 题解

本题是动态规划

用dp\[i][j]表示nums的i~j之间的最大差

初始状态：dp\[i][i]=nums[i]

状态转移方程：dp\[i][j]=max(nums[i]-dp\[i+1][j],nums[j]-dp\[i][j-1])

从状态转移方程可以看出，dp\[i][j]依赖于i+1和j-1，所以i从大到小遍历，j从小到大遍历

# 代码

```c++
//c++
//执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
//内存消耗：7.9 MB, 在所有 C++ 提交中击败了10.91%的用户

class Solution {
public:
    bool PredictTheWinner(vector<int>& nums) {
        int n=nums.size();
        vector<vector<int>> dp(n,vector<int>(n,0));
        for(int i=0;i<n;++i){
            dp[i][i]=nums[i];
        }
        for(int i=n-2;i>=0;--i)
            for(int j=i+1;j<n;++j){
                dp[i][j]=max(nums[i]-dp[i+1][j],nums[j]-dp[i][j-1]);
            }
        return dp[0][n-1]>=0;
    }
};
```


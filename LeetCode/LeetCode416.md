#### [416. 分割等和子集](https://leetcode-cn.com/problems/partition-equal-subset-sum/)

# 题目描述

给定一个只包含正整数的非空数组。是否可以将这个数组分割成两个子集，使得两个子集的元素和相等。

注意:

1. 每个数组中的元素不会超过 100
2. 数组的大小不会超过 200

# 示例

```
输入: [1, 5, 11, 5]

输出: true

解释: 数组可以分割成 [1, 5, 5] 和 [11].
```

```
输入: [1, 2, 3, 5]

输出: false

解释: 数组不能分割成两个元素和相等的子集.
```

# 题解

本题和0-1背包问题的思想差不多，但是也有一些区别,本题在初始化的时候是初始化为false，采用动态规划的解法，用dp\[i][j]表示nums[0]~nums[i-1]i个数字中是否能组成和为j

# 代码

```c++
//c++
//执行用时：608 ms, 在所有 C++ 提交中击败了32.86%的用户
//内存消耗：11.1 MB, 在所有 C++ 提交中击败了17.39%的用户

class Solution {
public:
    bool canPartition(vector<int>& nums) {
        int n=nums.size();
        if(n==0)
            return false;
        //用sum表示数组的和
        int sum=0;
        for(int num:nums)
            sum+=num;
        sum必须得是偶数，否则不可能存在解，返回false
        if(sum&1==1)
            return false;
        int target=sum/2;
        //dp[i][j]表示1-i个数是否能和为j
        vector<vector<bool>> dp(n+1,vector<bool>(target+1,false));
        //初始状态,不太好推，可以举例
        for(int i=0;i<=n;++i){
            dp[i][0]=true;
        }
        for(int i=1;i<=n;++i)
            for(int j=1;j<=target;++j){
                if(j<nums[i-1])
                    dp[i][j]=dp[i-1][j];
                else
                    dp[i][j]=dp[i-1][j]||dp[i-1][j-nums[i-1]];  
            }
        return dp[n][target];
    }
};
```


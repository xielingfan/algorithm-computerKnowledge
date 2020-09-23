#### [300. 最长上升子序列](https://leetcode-cn.com/problems/longest-increasing-subsequence/)

# 题目描述

给定一个无序的整数数组，找到其中最长上升子序列的长度。



# 示例

```
输入: [10,9,2,5,3,7,101,18]
输出: 4 
解释: 最长的上升子序列是 [2,3,7,101]，它的长度是 4。
```



# 题解

此题是典型的动态规划题目，设置dp数组，初始条件为dp[i]=1,0<i<nums.size(),对于每一个nums[i]，从nums[0]~nums[i-1]与nums[i]进行对比，if(nums[j]<nums[i]) 那么一定能组成上升序列，此时dp[i]=max(dp[j]+1,dp[i]);



# 代码

```c++
//c++
//执行用时：104 ms, 在所有 C++ 提交中击败了27.24%的用户
//内存消耗：7.4 MB, 在所有 C++ 提交中击败了95.02%的用户

class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        int n=nums.size();
        if(n==0) return 0;
        //初始状态全为1
        vector<int> dp(n,1);
        int ans=1;
        for(int i=1;i<n;++i){
            for(int j=0;j<i;++j){
                if(nums[j]<nums[i])
                	//状态转移方程
                    dp[i]=max(dp[j]+1,dp[i]);
            }
            ans=max(ans,dp[i]);
        }
        return ans;
    }
};
```


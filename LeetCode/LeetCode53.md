#### [53.最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

# 题目描述

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

# 题解

动态规划例题。对数组进行遍历，寻找以元素 i 为结尾的最大子序和，转移方程为 ![image-20200925123129561](/Users/zhongyiming/Library/Application Support/typora-user-images/image-20200925123129561.png)

# 代码

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        //判空
        if (!nums.size())
            return 0;
        //正文
        int mlist[nums.size()];
        int maxsum = mlist[0] = nums[0];
        
        for (int i = 1;i < nums.size();i++) {
            mlist[i] = max(mlist[i-1] + nums[i],nums[i]);
            maxsum = max(maxsum,mlist[i]);
        }
        printf("maxsum = %d\n",maxsum);
        return maxsum;

    }
};

```


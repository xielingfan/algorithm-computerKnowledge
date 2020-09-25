#### [377. 组合总和 Ⅳ](https://leetcode-cn.com/problems/combination-sum-iv/)

# 题目描述

给定一个由正整数组成且不存在重复数字的数组，找出和为给定目标正整数的组合的个数。



# 示例

```
nums = [1, 2, 3]
target = 4

所有可能的组合为：
(1, 1, 1, 1)
(1, 1, 2)
(1, 2, 1)
(1, 3)
(2, 1, 1)
(2, 2)
(3, 1)

因此输出为 7。
```



# 代码

```c++
//c++
//执行用时：4 ms, 在所有 C++ 提交中击败了66.95%的用户
//内存消耗：6.7 MB, 在所有 C++ 提交中击败了83.40%的用户

class Solution {
public:
    int combinationSum4(vector<int> &nums,int target){
        int n=nums.size();
        if(n<=0)return 0;
        vector<unsigned int> dp(target+1,0);
        dp[0]=1;
        for(int i=1;i<=target;++i){
            for(int j=0;j<n;++j){
                if(i-nums[j]>=0)
                    dp[i]+=dp[i-nums[j]];
            }
        }
        return dp[target];
    }
};
```


#### [343. 整数拆分](https://leetcode-cn.com/problems/integer-break/)

# 题目描述

给定一个正整数 *n*，将其拆分为**至少**两个正整数的和，并使这些整数的乘积最大化。 返回你可以获得的最大乘积。

# 示例

```
输入: 2
输出: 1
解释: 2 = 1 + 1, 1 × 1 = 1。
```

```
输入: 10
输出: 36
解释: 10 = 3 + 3 + 4, 3 × 3 × 4 = 36。
```

# 题解

采用动态规划求解，创建数组dp，dp[i]表示正整数i拆分后可得的最大乘积。对于正整数i，当i>=2时，可以进行拆分，假设拆为j和i-j，而i-j可以进行拆分，也可以不进行拆分，那么对于i来说，dp[i]=max(dp[i-j]\*j,(i-j)\*j),1<=j<i;dp[0]=dp[1]=0

# 代码

```c++
//c++
//执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
//内存消耗：6 MB, 在所有 C++ 提交中击败了50.28%的用户

class Solution {
public:
    int integerBreak(int n) {
        vector<int>dp(n+1);
        for(int i=2;i<=n;++i){
            for(int j=1;j<i;++j)
                dp[i]=max(dp[i],max((i-j)*j,j*dp[i-j]));
        }
        return dp[n];
    }
};
```




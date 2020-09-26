#### [581. 最短无序连续子数组](https://leetcode-cn.com/problems/shortest-unsorted-continuous-subarray/)

# 题目描述

给定一个整数数组，你需要寻找一个**连续的子数组**，如果对这个子数组进行升序排序，那么整个数组都会变为升序排序。

你找到的子数组应是**最短**的，请输出它的长度。

```
输入: [2, 6, 4, 8, 10, 9, 15]
输出: 5
解释: 你只需要对 [6, 4, 8, 10, 9] 进行升序排序，那么整个表都会变为升序排序。
```

# 题解

可以复制一个nums，先排序，再与原数组进行比较，左边第一个不一样的和右边第一个不一样的之间就是需要排序的数字。



# 代码

```c++
//c++
//执行用时：108 ms, 在所有 C++ 提交中击败了31.76%的用户
//内存消耗：25.6 MB, 在所有 C++ 提交中击败了37.41%的用户

class Solution {
public:
    int findUnsortedSubarray(vector<int>& nums) {
        vector<int> v=nums;
        sort(v.begin(),v.end());
        int l=0,r=0;
        for(int i=0;i<nums.size();++i){
            if(v[i]!=nums[i]){
                l=i;
                break;
            }
        }
        for(int i=nums.size()-1;i>=0;--i){
            if(v[i]!=nums[i]){
                r=i;
                break;
            }
        }
        if(l==r)
            return 0;
        return r-l+1;
    }
};
```




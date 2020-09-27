#### [347. 前 K 个高频元素](https://leetcode-cn.com/problems/top-k-frequent-elements/)

# 题目描述

给定一个非空的整数数组，返回其中出现频率前 ***k\*** 高的元素。

# 示例

```
输入: nums = [1,1,1,2,2,3], k = 2
输出: [1,2]
```

# 题解

用map存储，再进行排序，这里要注意对map进行按value的排序需要用到vector，不能直接用sort排序.

# 代码

```c++
//c++
//执行用时：48 ms, 在所有 C++ 提交中击败了35.73%的用户
//内存消耗：13.7 MB, 在所有 C++ 提交中击败了48.86%的用户

class Solution {
public:
    static bool cmp(pair<int,int> a,pair<int,int> b){
        return a.second>b.second;
    }
    vector<int> topKFrequent(vector<int>& nums, int k) {
        map<int,int> mp;
        vector<int> ans;
        for(int i=0;i<nums.size();++i){
            int x=nums[i];
            ++mp[x];
        }
        vector<pair<int,int>>v;
        //将mp中的每一个pair存入vector
        for(auto m:mp){
            v.push_back(m);
        }
        sort(v.begin(),v.end(),cmp);
        for(int i=0;i<k;++i)
            ans.push_back(v[i].first);
        return ans;
    }
};
```


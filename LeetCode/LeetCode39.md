#### [39. 组合总和](https://leetcode-cn.com/problems/combination-sum/)

# 题目描述

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

1. 所有数字（包括 target）都是正整数。
2. 解集不能包含重复的组合。 

# 示例

```c++
输入：candidates = [2,3,6,7], target = 7,
所求解集为：
[
  [7],
  [2,2,3]
]
```

```c++
输入：candidates = [2,3,5], target = 8,
所求解集为：
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

# 题解

本题属于排列组合问题，使用回溯算法，一般情况下，排列问题的i从0开始迭代，组合问题的i从index开始迭代，本题也不例外。

但是，题目要求candidates中的数字可以无限制重复被选取，那么只需要在index应该+1的情况下不+1；

# 代码

```c++
//c++
//执行用时：12ms
//内存消耗：10.7 MB

class Solution {
public:
    void backtrack(vector<vector<int>> &ans,const vector<int> &candidates,const int &target,vector<int> &curv,int &cursum,int index){
        if(index>candidates.size())
            return;
        if(cursum==target){
            ans.push_back(curv);
            return;
        }
        if(cursum<target){
            for(int i=index;i<candidates.size();++i){
                cursum+=candidates[i];
                curv.push_back(candidates[i]);
                //与一般的组合问题只有这里不一样，一般组合是  backtrack(ans,candidates,target,curv,cursum,i+1)，这里i+1了
                backtrack(ans,candidates,target,curv,cursum,i);
                cursum-=candidates[i];
                curv.pop_back();
            }
        }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<vector<int>> ans;
        //curv表示当前的vector
        vector<int> curv;
        int cursum=0;
        backtrack(ans,candidates,target,curv,cursum,0);
        return ans;
    }
};
```


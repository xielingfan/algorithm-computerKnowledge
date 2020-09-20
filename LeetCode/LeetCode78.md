题目链接：https://leetcode-cn.com/problems/subsets/submissions/

```c++
//c++
//执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
//内存消耗：6.9 MB, 在所有 C++ 提交中击败了60.18%的用户
//通过限制便利起始条件，将遍历次数降至最低，即每次dfs都产生一个有意义的结果，不做任何无用的尝试
class Solution {
public:
    void dfs(vector<int>& nums, int start, int end, vector<int>& path, vector<vector<int>>& res) {
        for(int i = start; i < end; ++i) {
            path.push_back(nums[i]);
            res.push_back(path);
            if(i + 1 < end) {
                dfs(nums, i + 1, end, path, res); //往后遍历，避免无用尝试
            }
            path.pop_back();
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        vector<vector<int>> res; //存储答案
        vector<int> path; //临时路径
        res.push_back(path); //空集也算子集
        dfs(nums, 0, nums.size(), path, res);
        return res;
    }
};
```


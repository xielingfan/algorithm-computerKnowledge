```c++
//给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。 
//
// candidates 中的每个数字在每个组合中只能使用一次。 
//
// 说明： 
//
// 
// 所有数字（包括目标数）都是正整数。 
// 解集不能包含重复的组合。 
// 
//
// 示例 1: 
//
// 输入: candidates = [10,1,2,7,6,1,5], target = 8,
//所求解集为:
//[
//  [1, 7],
//  [1, 2, 5],
//  [2, 6],
//  [1, 1, 6]
//]
// 
//
// 示例 2: 
//
// 输入: candidates = [2,5,2,1,2], target = 5,
//所求解集为:
//[
//  [1,2,2],
//  [5]
//] 
// Related Topics 数组 回溯算法 
// 👍 406 👎 0


//c++
//执行用时：8 ms, 在所有 C++ 提交中击败了89.92%的用户
//内存消耗：11 MB, 在所有 C++ 提交中击败了56.01%的用户
class Solution {
private:
    vector<vector<int>> res;
public:
    void dfs(vector<int>& candidates, int nowsum, int target, vector<int>& path, int canbegin) {
        for(int i = canbegin; i < candidates.size(); ++i) {
            int newsum = nowsum + candidates[i];
            if(newsum < target) {
                path.push_back(candidates[i]);
                dfs(candidates, newsum, target, path, i);
                path.pop_back();
            }
            else if(newsum == target) {
                path.push_back(candidates[i]);
                res.push_back(path);
                path.pop_back();
            }
            else {
                return;
            }
        }
    }
    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        vector<int> path;
        sort(candidates.begin(), candidates.end());
        dfs(candidates, 0, target, path, 0);
        return res;
    }
};
//leetcode submit region end(Prohibit modification and deletion)
```
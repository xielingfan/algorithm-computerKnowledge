#### [78. 子集](https://leetcode-cn.com/problems/subsets/)

# 题目描述

给定一组**不含重复元素**的整数数组 nums，返回该数组所有可能的子集（幂集）。

**说明**：解集不能包含重复的子集。

**示例:**

```
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

# 代码

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

```java
//java
//执行用时：1 ms, 在所有 Java 提交中击败了99.39%的用户
//内存消耗：39.4 MB, 在所有 Java 提交中击败了8.07%的用户
//通过位运算遍历所有情况

class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        int len = nums.length;
        for (int i = 0; i < (1 << len); i++) {
            List<Integer> sub = new ArrayList<Integer>();
            for (int j = 0; j < nums.length; j++)
                if (((i >> j) & 1) == 1)
                    sub.add(nums[j]);
            res.add(sub);
        }
        return res;
    }
}
```

```java
//java
//执行用时：1 ms, 在所有 Java 提交中击败了99.39%的用户
//内存消耗：39 MB, 在所有 Java 提交中击败了67.09%的用户
//回溯法
class Solution {
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> res = new ArrayList<List<Integer>>();
        backtrack(res,new ArrayList<>(), nums, 0);
        return res;
    }

    private void backtrack(List<List<Integer>> list, List<Integer> tempList, int[] nums, int start)     {
        //走过的所有路径都是子集的一部分，所以都要加入到集合中
        list.add(new ArrayList<>(tempList));
        for (int i = start; i < nums.length; i++) {
            //做出选择
            tempList.add(nums[i]);
            //递归
            backtrack(list, tempList, nums, i + 1);
            //撤销选择
            tempList.remove(tempList.size() - 1);
        }
    }
}
```


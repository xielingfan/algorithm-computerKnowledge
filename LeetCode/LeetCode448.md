#### [448. 找到所有数组中消失的数字](https://leetcode-cn.com/problems/find-all-numbers-disappeared-in-an-array/)

# 题目

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

# 示例

```
输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```



# 题解

使用vis来判断是否访问过，最后遍历vis数组



# 代码

```c++
//c++
//执行用时：120 ms, 在所有 C++ 提交中击败了68.04%的用户
//内存消耗：32.4 MB, 在所有 C++ 提交中击败了17.35%的用户

class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> ans;
        int n=nums.size();
        vector<int> vis(n+1,0);
        for(int i=0;i<n;++i){
            vis[nums[i]]=1;
        }
        for(int i=1;i<=n;++i){
            if(vis[i]==0)
                ans.push_back(i);
        }
        return ans;
    }
};
```


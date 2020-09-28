```c++
//给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。 
//
// 按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下： 
//
// 
// "123" 
// "132" 
// "213" 
// "231" 
// "312" 
// "321" 
// 
//
// 给定 n 和 k，返回第 k 个排列。 
//
// 说明： 
//
// 
// 给定 n 的范围是 [1, 9]。 
// 给定 k 的范围是[1, n!]。 
// 
//
// 示例 1: 
//
// 输入: n = 3, k = 3
//输出: "213"
// 
//
// 示例 2: 
//
// 输入: n = 4, k = 9
//输出: "2314"
// 
// Related Topics 数学 回溯算法 
// 👍 403 👎 0


//c++
//执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
//内存消耗：5.9 MB, 在所有 C++ 提交中击败了67.24%的用户
//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
public:
    string ans;
    int nums[10];
    int flag[10] = {0};
    void dfs(int total, int n, int k) {
        if(k == 1) {
            for(int i = 1; i <= total; ++i) {
                if(!flag[i]) {
                    ans.push_back(i + '0');
                }
            }
            return;
        }
        int i;
        for(i = 1; i <=9; ++i) {
            if(flag[i]) {
                continue;
            }
            if(k > nums[n - 1]) {
                k -= nums[n - 1];
            } else {
                break;
            }
        }
        flag[i] = 1;
        ans.push_back(i + '0');
        dfs(total, n - 1, k);
    }
    string getPermutation(int n, int k) {
        int cnt = 1;
        for(int i = 1; i < 10; ++i) {
            cnt *= i;
            nums[i] = cnt;
        }
        dfs(n, n, k);
        return ans;
    }
};
//leetcode submit region end(Prohibit modification and deletion)
```


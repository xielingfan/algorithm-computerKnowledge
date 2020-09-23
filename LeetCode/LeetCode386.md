```java
//给定一个整数 n, 返回从 1 到 n 的字典顺序。 
//
// 例如， 
//
// 给定 n =1 3，返回 [1,10,11,12,13,2,3,4,5,6,7,8,9] 。 
//
// 请尽可能的优化算法的时间复杂度和空间复杂度。 输入的数据 n 小于等于 5,000,000。 
// 👍 128 👎 0


//leetcode submit region begin(Prohibit modification and deletion)
class Solution {
    List<Integer> res = new ArrayList<>();
    public void dfs(int now, int n) {
        now *= 10;
        int diff = n - now;
        if(diff < 0) {
            return;
        }
        for(int i = 0; i < 10 && i <= diff; ++i) {
            int temp = now + i;
            res.add(temp);
            dfs(temp, n);
        }
    }
    public List<Integer> lexicalOrder(int n) {
        for(int i = 1; i < 10 && i <= n; ++i) {
            res.add(i);
            dfs(i, n);
        }
        return res;
    }
}
//leetcode submit region end(Prohibit modification and deletion)

```


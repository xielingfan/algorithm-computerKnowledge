```python
# 给你一个由一些多米诺骨牌组成的列表 dominoes。 
# 
#  如果其中某一张多米诺骨牌可以通过旋转 0 度或 180 度得到另一张多米诺骨牌，我们就认为这两张牌是等价的。 
# 
#  形式上，dominoes[i] = [a, b] 和 dominoes[j] = [c, d] 等价的前提是 a==c 且 b==d，或是 a==d 且 
# b==c。 
# 
#  在 0 <= i < j < dominoes.length 的前提下，找出满足 dominoes[i] 和 dominoes[j] 等价的骨牌对 (i,
#  j) 的数量。 
# 
#  
# 
#  示例： 
# 
#  输入：dominoes = [[1,2],[2,1],[3,4],[5,6]]
# 输出：1
#  
# 
#  
# 
#  提示： 
# 
#  
#  1 <= dominoes.length <= 40000 
#  1 <= dominoes[i][j] <= 9 
#  
#  Related Topics 数组 
#  👍 32 👎 0


#Python3
#执行耗时:284 ms,击败了86.72% 的Python3用户
#内存消耗:22.7 MB,击败了52.89% 的Python3用户
# leetcode submit region begin(Prohibit modification and deletion)
class Solution:
    def numEquivDominoPairs(self, dominoes: List[List[int]]) -> int:
        ans = 0
        d = collections.defaultdict(int)
        for i, j in dominoes:
            num = 10 * i + j if i < j else 10 * j + i
            d[num] += 1
        for k in d.values():
            ans += int(k * (k - 1) / 2)
        return ans
# leetcode submit region end(Prohibit modification and deletion)
```


#### [461. 汉明距离](https://leetcode-cn.com/problems/hamming-distance/)



# 题目描述

两个整数之间的[汉明距离](https://baike.baidu.com/item/汉明距离)指的是这两个数字对应二进制位不同的位置的数目。

给出两个整数 `x` 和 `y`，计算它们之间的汉明距离。

# 示例

```
输入: x = 1, y = 4

输出: 2

解释:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
```

# 题解

可以对x，y的每一个最右边的位进行比较，如果不等，++ans

还有另一种方法，另n=x^y，这样只需要统计n中1的个数就好了，统计1的个数可以利用n&=(n-1)，n&(n-1)表示去掉n最右边的1之后的数。



# 代码

```c++
//c++
//执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
//内存消耗：5.7 MB, 在所有 C++ 提交中击败了74.90%的用户

class Solution {
public:
    int hammingDistance(int x, int y) {
        int ans=0;
        while(x||y){
        //在这里要特别注意，==的优先级是高于&，所以必须加括号
            if((x&1)==1&&(y&1)==0)
                ++ans;
            if((x&1)==0&&(y&1)==1)
                ++ans;
            x>>=1;
            y>>=1;
        }
        return ans;
    }
};

//第二种方法
class Solution {
public:
    int hammingDistance(int x, int y) {
        int n=x^y;
        int ans=0;
        while(n){
            n&=(n-1);
            ++ans;
        }
        return ans;
    }
};
```


#### [739. 每日温度](https://leetcode-cn.com/problems/daily-temperatures/)

# 题目描述

请根据每日 气温 列表，重新生成一个列表。对应位置的输出为：要想观测到更高的气温，至少需要等待的天数。如果气温在这之后都不会升高，请在该位置用 0 来代替。

# 示例

```c++
输入：
	temperatures = [73, 74, 75, 71, 69, 72, 76, 73]
输出：
	[1, 1, 4, 2, 1, 1, 0, 0]
```

# 代码

```c++
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& T) {
        int n=T.size();
        vector<int> ans(n,0);
        stack<int> s;
        for(int i=n-1;i>=0;--i){
            while(!s.empty()&&T[i]>=T[s.top()])
                s.pop();
            if(s.empty())
                ans[i]=0;
            else
                ans[i]=s.top()-i;
            s.push(i);
        }
        return ans;
    }

};
```


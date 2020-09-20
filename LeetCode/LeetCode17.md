#### [17. 电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

# 题目描述

给定一个仅包含数字 `2-9` 的字符串，返回所有它能表示的字母组合。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

# 题解

本题是典型的回溯题，回溯题的一般模板是：

```c++
void backtrack(ans,cur,start,end){
	if(start==end){
		//得到一个答案，保存
		ans.push(cur);
		return;
	}
	for(int i=start,i<end;++i){
		满足某种条件（可有可无）;
		cur.push(x);
		backtrack(ans,cur,start+1,end);
		cur.pop();
	}
}
```

本题只需要把数字对应的string保存起来，然后进行回溯即可

# 代码

```c++
void backtrack(vector<string>& vs, vector<string> &ans, string &digits, string &cur, int index) {
	if (index == digits.size()) {
		//得到一个解
		ans.push_back(cur);
		return;
	}
	//k用来表示digits数组中的数字，将digits[i]转为int类型
	int k = digits[index] - '0';
	for (int i = 0; i < vs[k].size(); ++i) {
		string s = vs[k];
		//string类型只重载了‘+’，没有重载‘-’，所以用pop_back()代替。
		cur += s[i];
		backtrack(vs, ans, digits, cur, index + 1);
		cur.pop_back();
	}

}
    vector<string> letterCombinations(string digits) {
        vector<string>ans;
        if(digits.size()<=0)
            return ans;
        //将映射保存起来
	    vector<string> vs(10);
	    vs[2] = "abc";
	    vs[3] = "def";
	    vs[4] = "ghi";
	    vs[5] = "jkl";
	    vs[6] = "mno";
	    vs[7] = "pqrs";
	    vs[8] = "tuv";
	    vs[9] = "wxyz";
	    string cur = "";
	    backtrack(vs, ans, digits, cur, 0);//递归回溯
	    return ans;
}
```




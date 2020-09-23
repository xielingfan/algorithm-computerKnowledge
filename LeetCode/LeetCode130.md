#### [130. 被围绕的区域](https://leetcode-cn.com/problems/surrounded-regions/)

# 题目

给定一个二维的矩阵，包含 `'X'` 和 `'O'`（**字母 O**）。

找到所有被 `'X'` 围绕的区域，并将这些区域里所有的 `'O'` 用 `'X'` 填充。

# 示例

```
X X X X
X O O X
X X O X
X O X X
```

运行你的函数后，矩阵变为：

```c++
X X X X
X X X X
X X X X
X O X X
```

# 题解

矩阵中的字符包含三种类型：

1. X
2. 被X包围的O，要转换为X
3. 没有被包围的O

可以在矩阵的最外层一圈进行dfs（O），这样它肯定是没有被包围的，并标记一下，比如转换为A，最后再设置回O。最后再遍历整个矩阵，如果为A，就转换为O，否则为X

# 代码

```c++
//c++
//运行时间：32ms
//运行内存：9.8MB

class Solution {
public:
    void dfs(vector<vector<char>> &board,int x,int y){
        int n=board.size();
        int m=board[0].size();
        if(x<0||x>=n||y<0||y>=m||board[x][y]!='O')
            return;
        board[x][y]='A';
        dfs(board,x+1,y);
        dfs(board,x-1,y);
        dfs(board,x,y+1);
        dfs(board,x,y-1);
    }
    void solve(vector<vector<char>> &board){
        int n=board.size();
        if(n==0)
            return;
        int m=board[0].size();
        //board为n行m列的矩阵
        for(int i=0;i<n;++i){
            //dfs第一列
            dfs(board,i,0);
            //dfs最后一列
            dfs(board,i,m-1);
        }
        for(int i=0;i<m;++i){
            //dfs第一行
            dfs(board,0,i);
            //dfs最后一行
            dfs(board,n-1,i);
        }
        for(int i=0;i<n;++i){
            for(int j=0;j<m;++j){
                //如果为A，说明是与边界连通的O替换的，所以要替换回去
                if(board[i][j]=='A'){
                    board[i][j]='O';
                }
                else if(board[i][j]=='O')
                    board[i][j]='X';
            }
        }
    }
};
```


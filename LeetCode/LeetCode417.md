#### [417. 太平洋大西洋水流问题](https://leetcode-cn.com/problems/pacific-atlantic-water-flow/)

# 题目描述

给定一个 m x n 的非负整数矩阵来表示一片大陆上各个单元格的高度。“太平洋”处于大陆的左边界和上边界，而“大西洋”处于大陆的右边界和下边界。

规定水流只能按照上、下、左、右四个方向流动，且只能从高到低或者在同等高度上流动。

请找出那些水流既可以流动到“太平洋”，又能流动到“大西洋”的陆地单元的坐标。

 

提示：

- 输出坐标的顺序不重要
- m 和 n 都小于150

# 示例

给定下面的 5x5 矩阵:

```
  太平洋 ~   ~   ~   ~   ~ 
       ~  1   2   2   3  (5) *
       ~  3   2   3  (4) (4) *
       ~  2   4  (5)  3   1  *
       ~ (6) (7)  1   4   5  *
       ~ (5)  1   1   2   4  *
          *   *   *   *   * 大西洋
  返回:
  [[0, 4], [1, 3], [1, 4], [2, 2], [3, 0], [3, 1], [4, 0]] (上图中带括号的单元).
```

# 题解

由于最外围的点一定能流入太平洋或者大西洋，所以能流到这点的其他点也能流入太平洋或者大西洋，用逆流的思想进行dfs

# 代码

```c++
//c++
//运行时间：88ms，在所有 C++ 提交中击败了52.80%的用户
//运行内存：15.7MB,在所有 C++ 提交中击败了63.15%的用户
class Solution {
public:
    //上下左右四个方向
    int dx[4]={-1,1,0,0};
    int dy[4]={0,0,-1,1};
    vector<vector<int>> ans;
    void dfs(const vector<vector<int>> &matrix,int x,int y,vector<vector<bool>> &v){
        int m=matrix.size();
        int n=matrix[0].size();
        if(x<0||x>=m||y<0||y>=n||v[x][y])
            return;
        v[x][y]=true;
        for(int i=0;i<4;++i){
            int tx=x+dx[i];
            int ty=y+dy[i];
            if(tx<0||tx>=m||ty<0||ty>=n||v[tx][ty]||matrix[x][y]>matrix[tx][ty])
                continue;
            dfs(matrix,tx,ty,v);
        }
    }
    vector<vector<int>> pacificAtlantic(vector<vector<int>>& matrix) {
        int m=matrix.size();
        if(m<=0) return ans;
        int n=matrix[0].size();
        //用两个bool型矩阵判断当前节点是否能流入大西洋或者太平洋
        vector<vector<bool>> Pacific(m,vector<bool>(n,false));
        vector<vector<bool>> Atlantic(m,vector<bool>(n,false));
        //从四周开始dfs
        for(int i=0;i<m;++i){
            dfs(matrix,i,0,Pacific);
            dfs(matrix,i,n-1,Atlantic);
        }
        for(int j=0;j<n;++j){
            dfs(matrix,0,j,Pacific);
            dfs(matrix,m-1,j,Atlantic);
        }
        for(int i=0;i<m;++i){
            for(int j=0;j<n;++j){
                //如果大西洋和太平洋都能流入，就是一个解
                if(Pacific[i][j]&&Atlantic[i][j]){
                    vector<int> v={i,j};
                    ans.push_back(v);
                }
            }
        }
        return ans;
    }
};
```


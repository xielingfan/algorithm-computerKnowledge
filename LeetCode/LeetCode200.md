#### [200. 岛屿数量](https://leetcode-cn.com/problems/number-of-islands/)

# 题目

给你一个由 '1'（陆地）和 '0'（水）组成的的二维网格，请你计算网格中岛屿的数量。

岛屿总是被水包围，并且每座岛屿只能由水平方向或竖直方向上相邻的陆地连接形成。

此外，你可以假设该网格的四条边均被水包围。



# 题解

本题是一个典型的DFS类型题，定义一个vector\<vector\<bool>> vis，来表示节点是否访问过，如果grid\[i][j]=='1'，那么就进行DFS，否则不处理。当前节点如果是岛屿的话，对上下左右四个方向进行DFS。



# 代码

```c++
class Solution {
public:
	//定义上下左右四个方向
    int dir_x[4]={-1,1,0,0};
    int dir_y[4]={0,0,-1,1};
    void dfs(vector<vector<char>>& grid,vector<vector<bool>> &vis,int x,int y){
        int m=grid.size(),n=grid[0].size();
        //判断当前节点是否合法
        if(x<0||x>=m||y<0||y>=n||vis[x][y])
            return;
        vis[x][y]=true;
        if(grid[x][y]=='1'){
        	//对(x,y)的上下左右四个方向上的节点进行处理
            for(int i=0;i<4;++i){
                int tx=x+dir_x[i];
                int ty=y+dir_y[i];
                //判断节点是否合法
                if(tx<0||tx>=m||ty<0||ty>=n||vis[tx][ty])
                    continue;
                if(grid[tx][ty]=='1')
                    dfs(grid,vis,tx,ty);
            }
        }
    }
    int numIslands(vector<vector<char>>& grid) {
        if(grid.size()<=0)
            return 0;
        vector<vector<bool>> vis(grid.size(),vector<bool>(grid[0].size(),false));
        int ans=0;
        for(int i=0;i<grid.size();++i)
            for(int j=0;j<grid[0].size();++j){
                if(!vis[i][j]){
                    if(grid[i][j]=='1'){
                        ++ans;
                        dfs(grid,vis,i,j);
                    }
                }
            }
        return ans;
    }
};
```












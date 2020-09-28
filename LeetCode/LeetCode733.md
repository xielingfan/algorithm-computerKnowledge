#### [733. 图像渲染](https://leetcode-cn.com/problems/flood-fill/)



# 题目描述

有一幅以二维整数数组表示的图画，每一个整数表示该图画的像素值大小，数值在 0 到 65535 之间。

给你一个坐标 (sr, sc) 表示图像渲染开始的像素值（行 ，列）和一个新的颜色值 newColor，让你重新上色这幅图像。

为了完成上色工作，从初始坐标开始，记录初始坐标的上下左右四个方向上像素值与初始坐标相同的相连像素点，接着再记录这四个方向上符合条件的像素点与他们对应四个方向上像素值与初始坐标相同的相连像素点，……，重复该过程。将所有有记录的像素点的颜色值改为新的颜色值。

最后返回经过上色渲染后的图像。

# 示例

```
输入: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
输出: [[2,2,2],[2,2,0],[2,0,1]]
```

# 题解
此题可以很容易想到要用BFS方法进行递归。

BFS方法套路：
1. 首先判断当前节点是否满足条件，如果不满足就return
2. 否则，当前节点满足条件，那么对当前节点进行操作。

题目要求所有坐标的原像素都必须等于初始点的像素，不妨设preColor=image[sr][sc]。下面分析一下什么条件下当前节点不满足：
1. sr<0||sr>image.length
2. sc<0||sc>image[0].length
3. image[sr][sc]==newColor //说明当前节点已经访问过，防止重复访问，否则递归出不来
4. image[sr][sc]!=preColor //所有节点的原像素都需要和preColor相等



# 代码

```c++
//c++
//执行用时：12 ms, 在所有 C++ 提交中击败了92.16%的用户
//内存消耗：13.3 MB, 在所有 C++ 提交中击败了82.79%的用户

class Solution {
    void bfs(int[][] image,int x,int y,int newColor,int preColor){
        //首先判断当前节点是否满足条件，不满足条件的退出
        if(x<0||x>=image.length||y<0||y>=image[0].length||image[x][y]==newColor||image[x][y]!=preColor)
            return;
        //如果满足条件,就遍历当前节点的上下左右四个节点
        else{
            image[x][y]=newColor;
            bfs(image,x-1,y,newColor,preColor);
            bfs(image,x+1,y,newColor,preColor);
            bfs(image,x,y-1,newColor,preColor);
            bfs(image,x,y+1,newColor,preColor);
        }
        
    }
    public int[][] floodFill(int[][] image, int sr, int sc, int newColor) {
        bfs(image,sr,sc,newColor,image[sr][sc]);
        return image;
    }
}
```
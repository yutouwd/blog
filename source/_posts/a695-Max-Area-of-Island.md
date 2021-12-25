---
title: 695.Max Area of Island & 733.Flood Fill
tags:
  - leetcode
  - 广度优先
categories:
  - leetcode
  - mudium
copyright: true
comments: true
abbrlink: 3305314244
date: 2021-07-28 10:22:02
---
# 题目描述
两道题目比较相似，都可以用广度优先或深度优先。然后通过修改矩阵中的数值来判断这个点是否遍历过。


## 733

有一幅以二维整数数组表示的图画，每一个整数表示该图画的像素值大小，数值在 0 到 65535 之间。

给你一个坐标 (sr, sc) 表示图像渲染开始的像素值（行 ，列）和一个新的颜色值 newColor，让你重新上色这幅图像。

为了完成上色工作，从初始坐标开始，记录初始坐标的上下左右四个方向上像素值与初始坐标相同的相连像素点，接着再记录这四个方向上符合条件的像素点与他们对应四个方向上像素值与初始坐标相同的相连像素点，……，重复该过程。将所有有记录的像素点的颜色值改为新的颜色值。

最后返回经过上色渲染后的图像。

示例 1:

输入: 
image = [[1,1,1],[1,1,0],[1,0,1]]
sr = 1, sc = 1, newColor = 2
输出: [[2,2,2],[2,2,0],[2,0,1]]
解析: 
在图像的正中间，(坐标(sr,sc)=(1,1)),
在路径上所有符合条件的像素点的颜色都被更改成2。
注意，右下角的像素没有更改为2，
因为它不是在上下左右四个方向上与初始点相连的像素点。
注意:

image 和 image[0] 的长度在范围 [1, 50] 内。
给出的初始点将满足 0 <= sr < image.length 和 0 <= sc < image[0].length。
image[i][j] 和 newColor 表示的颜色值在范围 [0, 65535]内。


```C++
class Solution {
public:
    bool isNeedColor(vector<vector<int>>& image, int x, int y, int n, int m, int oriColor){
        if (x < 0 || x >= n || y < 0 || y >= m) return false;
        if (image[x][y] == oriColor) return true;
        return false;
    }

    vector<vector<int>> floodFill(vector<vector<int>>& image, int sr, int sc, int newColor) {
        queue<pair<int,int>> q;
        int n = image.size(), m = image[0].size();
        int oriColor = image[sr][sc];
        vector<vector<int>> res(image);
        q.push(make_pair(sr, sc));
        while(q.size()){
            int times = q.size();
            for (int i = 0; i < times; i++){
                auto cur = q.front();
                q.pop();
                int x = cur.first, y = cur.second;
                if (isNeedColor(image, x, y, n, m, oriColor)&&res[x][y]!=newColor){
                    res[x][y] = newColor;
                    q.push(make_pair(x-1,y));
                    q.push(make_pair(x+1,y));
                    q.push(make_pair(x,y-1));
                    q.push(make_pair(x,y+1));
                }
            }
        }
        return res;
    }
};

```

## 695


给定一个包含了一些 0 和 1 的非空二维数组 grid 。

一个 岛屿 是由一些相邻的 1 (代表土地) 构成的组合，这里的「相邻」要求两个 1 必须在水平或者竖直方向上相邻。你可以假设 grid 的四个边缘都被 0（代表水）包围着。

找到给定的二维数组中最大的岛屿面积。(如果没有岛屿，则返回面积为 0 。)

 

示例 1:

[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
对于上面这个给定矩阵应返回 6。注意答案不应该是 11 ，因为岛屿只能包含水平或垂直的四个方向的 1 。

示例 2:

[[0,0,0,0,0,0,0,0]]
对于上面这个给定的矩阵, 返回 0。

 

注意: 给定的矩阵grid 的长度和宽度都不超过 50。





```C++
class Solution {
public:
    int n,m;
    bool isValid(int x, int y){
        return (x >= 0 && x < n && y >= 0 && y < m);
    }
    
    int computeSize(vector<vector<int>>& island, int x, int y){
        queue<pair<int,int>> q;
        q.push(make_pair(x,y));
        int size = 0;
        while(q.size()){
            int times = q.size();
            for (int i = 0; i < times; i++){
                auto cur = q.front();
                q.pop();
                int cx = cur.first, cy = cur.second;
                if (isValid(cx, cy) && island[cx][cy] == 1){
                    size++;
                    island[cx][cy] = 0;
                    q.push(make_pair(cx+1,cy));
                    q.push(make_pair(cx-1,cy));
                    q.push(make_pair(cx,cy+1));
                    q.push(make_pair(cx,cy-1));
                }
            }
        }
        return size;
    }
    
    
    int maxAreaOfIsland(vector<vector<int>>& grid) {
        vector<vector<int>> island(grid);
        int res = 0;
        n = island.size();
        if (n == 0) return res;
        m = island[0].size();
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (island[i][j] == 0) continue;
                int curSize = computeSize(island, i, j);
                res = max(res, curSize);
            }
        }
        return res;
    }
};
```
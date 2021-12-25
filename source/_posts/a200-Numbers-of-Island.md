---
title: 200.Numbers of Island
tags:
  - leetcode
  - vector
  - 深度优先
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 1693659293
date: 2019-12-15 16:50:05
---
# 题目描述
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
Input:
11110
11010
11000
00000
Output: 1

Example 2:
Input:
11000
11000
00100
00011
Output: 3
# 我的解法
## 解题思路
用深度优先搜索
## 实现代码
```C++
class Solution {
public:
    void eraseIsland(vector<vector<char>>& grid, int i , int j){
        int n = grid.size(), m = grid[0].size();
        if (i < 0 || j < 0 || i == n || j == m || grid[i][j] == '0')
            return;
        grid[i][j] = '0';
        eraseIsland(grid, i + 1, j);
        eraseIsland(grid, i - 1, j);
        eraseIsland(grid, i, j + 1);
        eraseIsland(grid, i, j - 1);
    }
    
    int numIslands(vector<vector<char>>& grid) {
        if (grid.size() == 0)
            return 0;
        int n = grid.size(), m = grid[0].size(), island = 0;
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (grid[i][j] == '1'){
                    eraseIsland(grid, i, j);
                    island++;
                }
            }
        }
        return island;
    } 
};
```

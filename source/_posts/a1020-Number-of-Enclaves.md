---
title: 1020.Number of Enclaves
tags:
  - leetcode
  - 深度优先
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 3587513103
date: 2021-08-17 16:19:22
---
# 题目描述
给出一个二维数组 A，每个单元格为 0（代表海）或 1（代表陆地）。

移动是指在陆地上从一个地方走到另一个地方（朝四个方向之一）或离开网格的边界。

返回网格中无法在任意次数的移动中离开网格边界的陆地单元格的数量。

 

示例 1：

输入：[[0,0,0,0],[1,0,1,0],[0,1,1,0],[0,0,0,0]]
输出：3
解释： 
有三个 1 被 0 包围。一个 1 没有被包围，因为它在边界上。
示例 2：

输入：[[0,1,1,0],[0,0,1,0],[0,0,1,0],[0,0,0,0]]
输出：0
解释：
所有 1 都在边界上或可以到达边界。
 

提示：

1 <= A.length <= 500
1 <= A[i].length <= 500
0 <= A[i][j] <= 1
所有行的大小都相同

# 我的解法
## 解题思路
通过边界上的陆地进行深度优先遍历，把遍历过的陆地都置为0。最后再遍历一次整个数组，统计1个的个数。
## 实现代码

```C++
class Solution {
public:
    void dfs(vector<vector<int>>& grid, int i, int j){
        int n = grid.size(), m = grid[0].size();
        if (i < 0 || i >= n || j < 0 || j >= m || grid[i][j] == 0)
            return;
        grid[i][j] = 0;
        dfs(grid,i-1,j);
        dfs(grid,i+1,j);
        dfs(grid,i,j-1);
        dfs(grid,i,j+1);
    }
    int numEnclaves(vector<vector<int>>& grid) {
        int res = 0;
        int n = grid.size(), m = grid[0].size();
        for (int i = 0; i < n; i++){
            if (grid[i][0] == 1)
                dfs(grid, i, 0);
            if (grid[i][m-1] == 1)
                dfs(grid, i, m-1);
        }
        for (int j = 0; j < m; j++){
            if (grid[0][j] == 1)
                dfs(grid, 0, j);
            if (grid[n-1][j] == 1)
                dfs(grid, n-1, j);
        }
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (grid[i][j] == 1)
                    res++;
            }
        }
        return res;
    }
};

```


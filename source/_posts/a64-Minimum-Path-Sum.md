---
title: 64.Minimum Path Sum
tags:
  - leetcode
  - 动态规划
categories:
  - leetcode
  - medium
mathjax: true
copyright: true
comments: true
abbrlink: 3379915881
date: 2020-02-22 10:21:06
---
# 题目描述
Given a m x n grid filled with non-negative numbers, find a path from top left to bottom right which minimizes the sum of all numbers along its path.

Note: You can only move either down or right at any point in time.

Example:
Input:
[
  [1,3,1],
  [1,5,1],
  [4,2,1]
]
Output: 7
Explanation: Because the path 1→3→1→1→1 minimizes the sum.

# 我的解法
## 解题思路
如果做了[#62][1]和[#63][2]题的话这题就很简单了，同样还是只能往下和右走，不过不同的是每一点都有了一个代价，要找到一条代价最小的路径。第一列和第一行都只能从上一个点走过去，每个点的代价都等于自己的代价加上上一个点的路径代价。中间每点的状态转移方程如下：

$$ dp[i][j] = min(dp[i-1][j],dp[i][j-1]) + grid[i][j]$$

## 实现代码
```C++
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size(), n = grid[0].size();
        vector<vector<long long>> path(m, vector<long long>(n, 0));
        path[0][0] = grid[0][0];
        for (int i = 1; i < m; i++)
            path[i][0] = grid[i][0] + path[i - 1][0];
        for (int j = 1; j < n; j++)
            path[0][j] = grid[0][j] + path[0][j - 1];
        for (int i = 1; i < m; i++){
            for (int j = 1; j < n; j++){
                path[i][j] = min(path[i-1][j], path[i][j-1]) + grid[i][j];
            }
        }
        return path[m - 1][n - 1];
    }
};
```
Runtime: 8 ms, faster than 88.39% of C++ online submissions for Minimum Path Sum.
Memory Usage: 11.1 MB, less than 23.68% of C++ online submissions for Minimum Path Sum.

[1]:https://yutouwd.github.io/posts/1511993047
[2]:https://yutouwd.github.io/posts/1744891308
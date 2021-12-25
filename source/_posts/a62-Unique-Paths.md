---
title: 62.Unique Paths
tags:
  - leetcode
  - math
  - 动态规划
categories:
  - leetcode
  - medium
copyright: true
comments: true
mathjax: true
abbrlink: 1511993047
date: 2020-02-20 17:49:58
---
# 题目描述
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

How many possible unique paths are there?


Above is a 7 x 3 grid. How many possible unique paths are there?

Note: m and n will be at most 100.

Example 1:

Input: m = 3, n = 2
Output: 3
Explanation:
From the top-left corner, there are a total of 3 ways to reach the bottom-right corner:
1. Right -> Right -> Down
2. Right -> Down -> Right
3. Down -> Right -> Right

Example 2:
Input: m = 7, n = 3
Output: 28
# 我的解法
## 解题思路
找到一个m*n的网格从左上角到右下角到所有路径，只能往右和下走。因为只能往右和下走，所以第一行和第一列都只有1种走法，那么(2，2)这个地方就有2种走法，因为可以从(1,1)->(1,2)和(1,1)->(2,1)。其实每个点可以走的方法都是它左边方法加上上面的方法数。那么状态转移方程就是:
$$ dp[i][j] = dp[i-1][j] + dp[i][j-1] $$
## 实现代码
```C++
class Solution {
public:
    int uniquePaths(int m, int n) {
        vector<vector<int>> path(m, vector<int>(n, 1));
        for(int i = 1; i < m; i++){
            for (int j = 1; j < n; j++){
                path[i][j] = path[i - 1][j] + path[i][j - 1];
            }
        }
        return path[m - 1][n - 1];
    }
};
```
Runtime: 4 ms, faster than 56.48% of C++ online submissions for Unique Paths.
Memory Usage: 8.9 MB, less than 14.06% of C++ online submissions for Unique Paths.

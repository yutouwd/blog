---
title: 63.Unique Paths II
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
abbrlink: 1744891308
date: 2020-02-21 09:43:09
---
# 题目描述
A robot is located at the top-left corner of a m x n grid (marked 'Start' in the diagram below).

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked 'Finish' in the diagram below).

Now consider if some obstacles are added to the grids. How many unique paths would there be?



An obstacle and empty space is marked as 1 and 0 respectively in the grid.

Note: m and n will be at most 100.

Example 1:
Input:
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]
Output: 2

Explanation:
There is one obstacle in the middle of the 3x3 grid above.
There are two ways to reach the bottom-right corner:
1. Right -> Right -> Down -> Down
2. Down -> Down -> Right -> Right

# 我的解法
## 解题思路
和上一题一样，但是路径上可能有障碍物。如果障碍物是在最左边一列，那么在这一列下面点可走点路径就都是0条了。最上面一行也同理。如果障碍物在中间，那么就只是这个点可走的路径为0条。状态转移方程和上一题还是没有变：

$$ dp[i][j] = dp[i-1][j] + dp[i][j-1] $$

不过如果这个点是障碍物点话这个点的可行路径数就要等于0了。还有要注意的就是一些边界条件，比如只有一共就只有一个点、一行或一列的情况。
## 实现代码
```C++
class Solution {
public:
    int uniquePathsWithObstacles(vector<vector<int>>& obstacleGrid) {
        int m = obstacleGrid.size(), n = obstacleGrid[0].size();
        // 只有一个点
        if (m == 1 && n == 1)
            return obstacleGrid[0][0] == 1 ? 0 : 1;
        // 起点是障碍物
        if (obstacleGrid[0][0] == 1)
            return 0;
        vector<vector<long long>> path(m, vector<long long>(n, 1));
        for (int i = 1; i < m; i++){
            if (path[i - 1][0] == 0 || obstacleGrid[i][0] == 1)
                path[i][0] = 0;
        }
        for (int j = 1; j < n; j++){
            if (path[0][j - 1] == 0 || obstacleGrid[0][j] == 1)
                path[0][j] = 0;
        }
        for (int i = 1; i < m; i++){
            for (int j = 1; j < n; j++){
                if (obstacleGrid[i][j] == 1)
                    path[i][j] = 0;
                else
                    path[i][j] = path[i - 1][j] + path[i][j - 1];
            }
        }

        return path[m - 1][n - 1];
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Unique Paths II.
Memory Usage: 9.3 MB, less than 40.00% of C++ online submissions for Unique Paths II.
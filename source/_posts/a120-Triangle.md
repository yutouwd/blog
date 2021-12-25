---
title: 120.Triangle
tags:
  - leetcode
  - math
  - 动态规划
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 3362500974
date: 2020-02-23 12:18:08
---
# 题目描述
Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]
The minimum path sum from top to bottom is 11 (i.e., 2 + 3 + 5 + 1 = 11).

Note:

Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.

# 我的解法
## 解题思路
杨辉三角[#118][1]和最短路径[#64][2]的结合题目。还是使用动态规划的方法，在三角形边上的都等于上一个边上的点加上自身的代价，而三角形中间的点就等于在它上方的两个点中的最小的那个加上它的代价。
## 实现代码
```C++
class Solution {
public:
    int minimumTotal(vector<vector<int>>& triangle) {
        vector<vector<int>> path;
        int n = triangle.size();
        path.resize(n);
        path[0].push_back(triangle[0][0]);
        for (int i = 1; i < n; i++){
            path[i].resize(i + 1);
            path[i][0] = path[i-1][0] + triangle[i][0];
            path[i][i] = path[i-1][i-1] + triangle[i][i];
            for (int j = 1; j < i; j++){
                path[i][j] = min(path[i-1][j-1],path[i-1][j]) + triangle[i][j];
            }
        }
        int ans = *min_element(path[n-1].begin(), path[n-1].end());
        return ans;
    }
};

```
Runtime: 4 ms, faster than 96.47% of C++ online submissions for Triangle.
Memory Usage: 9.9 MB, less than 56.52% of C++ online submissions for Triangle.

[1]:https://yutouwd.github.io/posts/281994477
[2]:https://yutouwd.github.io/posts/3379915881
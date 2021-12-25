---
title: 73.Set Matrix Zeros
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 2772617193
date: 2020-12-14 16:49:01
---
# 题目描述
给定一个 m x n 的矩阵，如果一个元素为 0，则将其所在行和列的所有元素都设为 0。请使用原地算法。

示例 1:

输入: 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
输出: 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
示例 2:

输入: 
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
输出: 
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
进阶:

一个直接的解决方案是使用  O(mn) 的额外空间，但这并不是一个好的解决方案。
一个简单的改进方案是使用 O(m + n) 的额外空间，但这仍然不是最好的解决方案。
你能想出一个常数空间的解决方案吗？


# 我的解法
## 解题思路
只想到O(m+n)额外空间的做法，遍历一次矩阵，记录下需要置零的行和列。
## 实现代码
```C++
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        vector<int> row, col;
        for (int i = 0; i < matrix.size(); i++){
            for (int j = 0; j < matrix[i].size(); j++){
                if (matrix[i][j] == 0){
                    row.push_back(i);
                    col.push_back(j);
                }
            }
        }
        for (int i = 0; i < row.size(); i++){
            for (int j = 0; j < matrix[0].size(); j++)
                matrix[row[i]][j] = 0;
        }
        for (int j = 0; j < col.size(); j++){
            for (int i = 0; i < matrix.size(); i++)
                matrix[i][col[j]] = 0;
        }
    }
};
```
执行用时：28 ms, 在所有 C++ 提交中击败了92.49%的用户
内存消耗：13.4 MB, 在所有 C++ 提交中击败了22.54%的用户

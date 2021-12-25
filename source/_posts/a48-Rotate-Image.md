---
title: 48.Rotate Image
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 1761982827
date: 2019-09-30 14:17:14
---
# 题目描述
You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

Note:

You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:

Given input matrix = 
[
  [1,2,3],
  [4,5,6],
  [7,8,9]
],

rotate the input matrix in-place such that it becomes:
[
  [7,4,1],
  [8,5,2],
  [9,6,3]
]
Example 2:

Given input matrix =
[
  [ 5, 1, 9,11],
  [ 2, 4, 8,10],
  [13, 3, 6, 7],
  [15,14,12,16]
], 

rotate the input matrix in-place such that it becomes:
[
  [15,13, 2, 5],
  [14, 3, 4, 1],
  [12, 6, 8, 9],
  [16, 7,10,11]
]
# 我的解法
## 解题思路
其实把要转换的次数以及每次转换对应的位置找到规律就可以了
## 实现代码
```C++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        
        int n = matrix.size();
        for (int i = 0; i < n / 2; i++){
            for (int j = i; j < n - i - 1; j++){
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[n-j-1][i];
                matrix[n-j-1][i] = matrix[n-i-1][n-j-1];
                matrix[n-i-1][n-j-1] = matrix[j][n-i-1];
                matrix[j][n-i-1] = tmp;
            }
        }
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Rotate Image.
Memory Usage: 9 MB, less than 87.81% of C++ online submissions for Rotate Image.


也可以先上线翻转，再对角线翻转：

```C++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        if (n == 0) return;
        for (int i = 0; i < n / 2; i++){
            for (int j = 0; j < n; j++){
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[n-i-1][j];
                matrix[n-i-1][j] = tmp;
            }
        }
        for (int i = 0; i < n; i++){
            for (int j = i; j < n; j++){
                int tmp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = tmp;
            }
        }
    }
};
```
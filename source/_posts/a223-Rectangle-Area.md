---
title: 223.Rectangle Area
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 3099514846
date: 2019-09-19 11:27:40
---
# 题目描述
Find the total area covered by two rectilinear rectangles in a 2D plane.

Each rectangle is defined by its bottom left corner and top right corner as shown in the figure.

Rectangle Area

Example:
Input: A = -3, B = 0, C = 3, D = 4, E = 0, F = -1, G = 9, H = 2
Output: 45

Note:
Assume that the total area is never beyond the maximum possible value of int.

# 我的解法
## 解题思路
其实就是和求IOU类似，但是C++会遇到各种边界问题...提示中说总面积不会超过int的最大值，但是如果没有减去相交的面积时可能会超过int的最大值。
## 实现代码
```C++
class Solution {
public:
    int computeArea(int A, int B, int C, int D, int E, int F, int G, int H) {
        // 如果直接用max(0,...)后面两个相减的可能会超出int的下界
        int x = min(C,G) > max(A,E) ? min(C,G) - max(A,E) : 0;
        int y = min(D,H) > max(B,F) ? min(D,H) - max(B,F) : 0;
        return (C - A) * (D -B) - x * y + (G -E) * (H - F);
    }
};
```

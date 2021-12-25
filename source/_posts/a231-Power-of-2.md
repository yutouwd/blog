---
title: 231.Power of two
tags:
  - leetcode
categories:
  - leetcode
copyright: true
comments: true
abbrlink: 1808807184
date: 2021-08-21 10:34:52
---
# 题目描述
判断一个数是不是2的倍数。
# 我的解法
## 解题思路
通过(n & (n-1))是否等于零可以来判断一个数是不是2的倍数。(n & (n-1))会将最小位的1置零。
## 实现代码

```C++
class Solution {
public:
    bool isPowerOfTwo(int n) {
        return n > 0 && (n & (n-1)) == 0;
    }
};
```
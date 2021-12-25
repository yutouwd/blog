---
title: 326.Power of Three
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2084194376
date: 2019-09-14 18:26:08
---
# 题目描述
Given an integer, write a function to determine if it is a power of three.

Example 1:
Input: 27
Output: true

Example 2:
Input: 0
Output: false

Example 3:
Input: 9
Output: true

Example 4:
Input: 45
Output: false

Follow up:
Could you do it without using any loop / recursion?

# 我的解法
## 解题思路
求一个数是不是3的幂，想到的方法是将一个数不断的求模并且将n除以3，如果模不等于零就停止，判断n是不是等于1，如果不等于1那就不是3的幂。

## 实现代码

```C++
class Solution {
public:
    bool isPowerOfThree(int n) {
        if (n <= 0) return false;
        if (n == 1) return true;
        int mod = 0;
        while (mod == 0){
            mod = n % 3;
            n /= 3;
        }
        if (n == 0 && mod == 1)
            return true;
        else
            return false;
    }
};
```
Runtime: 16 ms, faster than 67.53% of C++ online submissions for Power of Three.
Memory Usage: 8.1 MB, less than 90.48% of C++ online submissions for Power of Three.

题目中还要求程序中不使用循环或者递归

# 高票解法
主要有两种方法
```C++
class Solution {
public:
    int const Max3PowerInt = 1162261467; // 3^19, 3^20 = 3486784401 > MaxInt32
    int const MaxInt32 = 2147483647; // 2^31 - 1
    bool isPowerOfThree(int n) {
        if (n <= 0 || n > Max3PowerInt) return false;
        return Max3PowerInt % n == 0;
    }
};
```
利用int的上限，求最大的3的幂，它除以n的模为零就说明n是3的幂

```C++
class Solution {
public:
    bool isPowerOfThree(int n) {
        if(n == 0) return false;
        double x = log10(n) / log10(3);
        return floor(x) == x;
    }
};
```
通过换底公式来判断。



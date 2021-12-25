---
title: 441.Arranging Coins
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 2997814324
date: 2020-03-23 19:20:40
---
# 题目描述
You have a total of n coins that you want to form in a staircase shape, where every k-th row must have exactly k coins.

Given n, find the total number of full staircase rows that can be formed.

n is a non-negative integer and fits within the range of a 32-bit signed integer.

Example 1:
n = 5

The coins can form the following rows:
¤
¤ ¤
¤ ¤

Because the 3rd row is incomplete, we return 2.

Example 2:
n = 8

The coins can form the following rows:
¤
¤ ¤
¤ ¤ ¤
¤ ¤

Because the 4th row is incomplete, we return 3.
# 我的解法
## 解题思路
比较笨的办法，不断将n减去行数。
```C++

class Solution {
public:
    int arrangeCoins(int n) {
        int i = 1;
        while (n > 0){
            if (n < i)
                return --i;
            n -= i++;
        }
        return --i;
    }
};
```

执行用时 :12 ms, 在所有 C++ 提交中击败了52.52%的用户
内存消耗 :7.2 MB, 在所有 C++ 提交中击败了100.00%的用户

其实可以直接用等差数列求和来求解

```C++

class Solution {
public:
    int arrangeCoins(int n) {
        return floor(-0.5+sqrt((double)2*n+0.25));
    }
};

```


执行用时 :4 ms, 在所有 C++ 提交中击败了89.51%的用户
内存消耗 :7.5 MB, 在所有 C++ 提交中击败了100.00%的用户

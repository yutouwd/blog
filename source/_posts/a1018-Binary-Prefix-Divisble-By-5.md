---
title: 1018.Binary Prefix Divisble By 5
tags:
  - leetcode
  - 位操作
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 2948955516
date: 2021-01-14 17:13:45
---
# 题目描述
Given an array A of 0s and 1s, consider N_i: the i-th subarray from A[0] to A[i] interpreted as a binary number (from most-significant-bit to least-significant-bit.)

Return a list of booleans answer, where answer[i] is true if and only if N_i is divisible by 5.

Example 1:
Input: [0,1,1]
Output: [true,false,false]
Explanation: 
The input numbers in binary are 0, 01, 011; which are 0, 1, and 3 in base-10.  Only the first number is divisible by 5, so answer[0] is true.

Example 2:
Input: [1,1,1]
Output: [false,false,false]

Example 3:
Input: [0,1,1,1,1,1]
Output: [true,false,false,false,true,false]

Example 4:
Input: [1,1,1,0,1]
Output: [false,false,false,false,false]

# 我的解法
## 解题思路
想法是用一个数来记录当前数字，到下一位时就将其左移一位，然后在加上A中对应位。不过数字会超出范围，看了下讨论发现可以用取10的模来避免越界，因为能被5整除的数只需要考虑最后一位是不是5或0即可。
## 实现代码

```C++
class Solution {
public:
    vector<bool> prefixesDivBy5(vector<int>& A) {
        int n = A.size();
        vector<bool> ans(n, false);
        if (n == 0) return ans;
        int num = 0;
        for (int i = 0; i < n; i++){
            num = num << 1;
            if (A[i] == 1) num++;
            ans[i] = (num % 5 == 0);
            num %= 10;
        }
        return ans;
    }
};
```

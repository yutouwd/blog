---
title: 191.Number of 1 Bits
tags:
  - leetcode
  - 位操作
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 100215024
date: 2020-02-29 17:08:35
---
# 题目描述
Write a function that takes an unsigned integer and return the number of '1' bits it has (also known as the Hamming weight).


Example 1:
Input: 00000000000000000000000000001011
Output: 3
Explanation: The input binary string 00000000000000000000000000001011 has a total of three '1' bits.

Example 2:
Input: 00000000000000000000000010000000
Output: 1
Explanation: The input binary string 00000000000000000000000010000000 has a total of one '1' bit.

Example 3:
Input: 11111111111111111111111111111101
Output: 31
Explanation: The input binary string 11111111111111111111111111111101 has a total of thirty one '1' bits.

# 我的解法
## 解题思路
一直都不太会位操作，参考了这篇题解：<https://leetcode.com/problems/number-of-1-bits/discuss/55255/C%2B%2B-Solution%3A-n-and-(n-1)>

## 实现代码

```C++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int count = 0;
        while(n){
            n &= (n - 1);
            count++;
        }
        return count;
    }
};

```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for Number of 1 Bits.
Memory Usage: 7.6 MB, less than 100.00% of C++ online submissions for Number of 1 Bits.

## 代码分析
用n和n-1按位与，效果如下面例子
| n | n-1 | n&(n-1) | count |
| --- | --- | --- | --- |
| 100101 | 100100 | 100100 | 1 |
| 100100 | 100011 | 100000 | 2 |
| 100000 | 011111 | 000000 | 3 |

刚好一个数字里面有几个1，就会进行几次与运算
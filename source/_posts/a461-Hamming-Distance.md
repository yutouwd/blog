---
title: 461.Hamming Distance
tags:
  - leetcode
  - 位操作
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 890411703
date: 2020-02-29 17:28:59
---
# 题目描述
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers x and y, calculate the Hamming distance.

Note:
0 ≤ x, y < 231.

Example:
Input: x = 1, y = 4
Output: 2
Explanation:
1   (0 0 0 1)
4   (0 1 0 0)
       ↑   ↑
The above arrows point to positions where the corresponding bits are different.
# 我的解法
## 解题思路
求两个数的汉明距离，即求两个二进制数之间有多少位是不同的。做了[#191][1]题之后，这题就很简单了。首先先把两个数按位异或，异或之后相同的位就是1，不同的位就是0。接下来就相当于求位1的个数了。
## 实现代码
```C++
class Solution {
public:
    int hammingDistance(int x, int y) {
        int ans = 0;
        int n = x ^ y;
        while(n){
            n &= (n - 1);
            ans++;
        }
        return ans;
    }
};
```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for Hamming Distance.
Memory Usage: 7.5 MB, less than 100.00% of C++ online submissions for Hamming Distance.

[1]:https://yutouwd.github.io/posts/100215024
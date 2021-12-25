---
title: 28.Implement strStr
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2690412730
date: 2019-05-22 22:41:03
---
# 题目描述
Implement strStr().

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

Example 1:
Input: haystack = "hello", needle = "ll"
Output: 2

Example 2:
Input: haystack = "aaaaa", needle = "bba"
Output: -1
# 我的解法
## 解题思路

## 实现代码
```C++
class Solution {
public:
    int strStr(string haystack, string needle){
        int len1 = haystack.length();
        int len2 = needle.length();
        for (int i = 0;i < len1-len2+1;i++){
            if (haystack.substr(i,len2) == needle){
                return i;
            }
        }
        return -1;
    }
};
```

Runtime: 8 ms, faster than 80.56% of C++ online submissions for Implement strStr().
Memory Usage: 9.3 MB, less than 53.68% of C++ online submissions for Implement strStr().



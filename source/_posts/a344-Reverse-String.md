---
title: 344.Reverse String
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 3640092658
date: 2019-08-08 20:34:44
---
# 题目描述
Write a function that reverses a string. The input string is given as an array of characters char[].

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

You may assume all the characters consist of printable ascii characters.

 

Example 1:

Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
Example 2:

Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
# 我的解法
## 实现代码
```C++
class Solution {
public:
    void reverseString(vector<char>& s) {
        int n = s.size();
        if (n <= 1) return;
        int i = 0, j = n - 1;
        while(i < j){
            swap(s[i++],s[j--]);
        }
    }
};
```

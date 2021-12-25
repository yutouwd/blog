---
title: 125.Valid Palindrome
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2448753357
date: 2019-09-23 18:26:06
---
# 题目描述
Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

Note: For the purpose of this problem, we define empty string as valid palindrome.

Example 1:
Input: "A man, a plan, a canal: Panama"
Output: true

Example 2:
Input: "race a car"
Output: false
# 我的解法
## 解题思路
题目其实挺简单的，就是实现的时候怎么能到简洁优雅，也是看了一个答案才知道。
## 实现代码
```C++
class Solution {
public:
    bool isPalindrome(string s) {
        int i = 0;
        int j = s.size() - 1;
        while (i < j){
            while ((i < j) && !(isdigit(s[i]) || isalpha(s[i] ))){
                i++;
            }
            while ((i < j) && !(isdigit(s[j]) || isalpha(s[j] ))){
                j--;
            }
            if (toupper(s[i]) != toupper(s[j]))
                return false;
            i++, j--;
        }
        return true;
    }
};
```

Runtime: 4 ms, faster than 99.21% of C++ online submissions for Valid Palindrome.
Memory Usage: 9.5 MB, less than 36.74% of C++ online submissions for Valid Palindrome.
# 知识总结
C++ 大小写转化、判断是不是字母的方法
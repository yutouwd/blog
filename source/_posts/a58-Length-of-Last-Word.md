---
title: 58.Length of Last Word
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 116524668
date: 2020-01-06 23:10:14
---
# 题目描述
Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word (last word means the last appearing word if we loop from left to right) in the string.
If the last word does not exist, return 0.

Note: A word is defined as a maximal substring consisting of non-space characters only.

Example:
Input: "Hello World"
Output: 5
# 我的解法
## 解题思路
想起了之前做过的一道题：[#824][1]可以使用istringstream来对一个字符串进行空格分割。
## 实现代码
```C++
class Solution {
public:
    int lengthOfLastWord(string s) {
        string tmp;
        istringstream ss(s);
        int len = 0;
        while(ss >> tmp){
            len = tmp.size();
        }
        return len;
    }
};
```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for Length of Last Word.
Memory Usage: 9.3 MB, less than 5.55% of C++ online submissions for Length of Last Word.

还可以把string先反转过来，就不需要再使用while循环了。
```C++
class Solution {
public:
    int lengthOfLastWord(string s) {
        reverse(s.begin(), s.end());
        istringstream ss(s);
        string res;
        ss >> res;
        return res.size();
    }
};
```
[1]:https://yutouwd.github.io/posts/316802933/
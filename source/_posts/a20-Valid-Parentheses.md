---
title: 20.Valid Parentheses
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 4278894845
date: 2019-09-26 13:46:24
---
# 题目描述
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example 1:
Input: "()"
Output: true

Example 2:
Input: "()[]{}"
Output: true

Example 3:
Input: "(]"
Output: false

Example 4:
Input: "([)]"
Output: false

Example 5:
Input: "{[]}"
Output: true

# 我的解法
## 解题思路
用一个string来做堆来储存左边的括号，如果遇到右边的括号就判断堆顶的左边括号和右边括号匹不匹配。
## 实现代码
```C++
class Solution {
public:
    bool isValid(string s) {
        if (s.size() % 2 != 0)
            return false;
        string tmp;
        for (int i = 0; i < s.size(); i++){
            if (s[i] == '(' || s[i] == '[' || s[i] == '{')
                tmp.push_back(s[i]);
            else{
                if ((s[i] == ')' && *(tmp.end() - 1) == '(') || (s[i] == '}' && *(tmp.end() - 1) == '{') || (s[i] == ']' && *(tmp.end() - 1) == '['))
                    tmp.pop_back();
                else
                    return false;
            }
        }
        if (tmp.size() != 0)
            return false;
        return true;
    }
};
```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for Valid Parentheses.
Memory Usage: 8.3 MB, less than 97.67% of C++ online submissions for Valid
虽然可以完成任务可以代码长了点

# 高票解法
## 实现代码
```C++
class Solution {
public:
    bool isValid(string s) {
        stack<char> paren;
        for (char & c : s){
            switch(c) {
                case '(':
                case '[':
                case '{': paren.push(c); break;
                case ')': if(paren.empty() || paren.top() != '(') return false; else paren.pop(); break;
                case ']': if(paren.empty() || paren.top() != '[') return false; else paren.pop(); break;
                case '}': if(paren.empty() || paren.top() != '{') return false; else paren.pop(); break;
                default: ;
            }
        }
        return paren.empty();
    }
};
```
## 代码分析
用switch case和stack就能整洁很多



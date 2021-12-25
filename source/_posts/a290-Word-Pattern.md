---
title: 290.Word Pattern
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 1795481488
date: 2020-12-16 16:17:21
---
# 题目描述
Given a pattern and a string s, find if s follows the same pattern.

Here follow means a full match, such that there is a bijection between a letter in pattern and a non-empty word in s.

Example 1:
Input: pattern = "abba", s = "dog cat cat dog"
Output: true

Example 2:
Input: pattern = "abba", s = "dog cat cat fish"
Output: false

Example 3:
Input: pattern = "aaaa", s = "dog cat cat dog"
Output: false

Example 4:
Input: pattern = "abba", s = "dog dog dog dog"
Output: false
 
Constraints:

1 <= pattern.length <= 300
pattern contains only lower-case English letters.
1 <= s.length <= 3000
s contains only lower-case English letters and spaces ' '.
s does not contain any leading or trailing spaces.
All the words in s are separated by a single space.
a w e
# 我的解法
## 解题思路
需要将pattern中的字符和s中里面的单词一一对应起来。使用一个map来记录每一个pattern对应的word，然后再使用一个set来记录已经有对应关系的word（防止一个word被多个pattarn对应）
## 实现代码
```C++
class Solution {
public:
    bool wordPattern(string pattern, string s) {
        vector<string> str;
        istringstream ss(s);
        unordered_map<char, string> m;
        unordered_set<string> k;
        string tmp;
        while(ss >> tmp)
            str.push_back(tmp);
        if (str.size() != pattern.size()) return false;
        for (int i = 0; i < pattern.size(); i++){
            if (m.find(pattern[i]) == m.end()){
                m.insert(make_pair(pattern[i], str[i]));
                if (k.find(str[i]) != k.end()){
                    return false;
                }
                k.insert(str[i]);
            }
            else{
                if (m[pattern[i]] != str[i])
                    return false;
            }
        }
        return true;
    }
};
```
执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
内存消耗：6.6 MB, 在所有 C++ 提交中击败了37.76%的用户


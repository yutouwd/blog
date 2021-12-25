---
title: 242.Valid Anagram
tags:
  - leetcode
  - string
  - hashmap
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 544546071
date: 2019-08-29 17:39:09
---
# 题目描述
Given two strings s and t , write a function to determine if t is an anagram of s.

Example 1:
Input: s = "anagram", t = "nagaram"
Output: true

Example 2:
Input: s = "rat", t = "car"
Output: false

Note:
You may assume the string contains only lowercase alphabets.

Follow up:
What if the inputs contain unicode characters? How would you adapt your solution to such case?

# 我的解法
## 解题思路
题目要求判断两个字符串是否是以同样的字符组成
## 实现代码
```C++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.size() != t.size()) return false;
        unordered_map<char, int> m1,m2;
        for (auto i : s) m1[i]++;
        for (auto i : t) m2[i]++;
        if (m1 == m2) return true;
        else return false;
    }
};
```

Runtime: 16 ms, faster than 55.14% of C++ online submissions for Valid Anagram.
Memory Usage: 9.5 MB, less than 74.63% of C++ online submissions for Valid Anagram.
# 高票解法
因为只有小写的字母，所以可以用一个数组来统计每个字符出现的次数
## 实现代码
```C++
class Solution {
public:
    bool isAnagram(string s, string t) {
        if (s.length() != t.length()) return false;
        int n = s.length();
        int counts[26] = {0};
        for (int i = 0; i < n; i++) { 
            counts[s[i] - 'a']++;
            counts[t[i] - 'a']--;
        }
        for (int i = 0; i < 26; i++)
            if (counts[i]) return false;
        return true;
    }
};
```

Runtime: 8 ms, faster than 97.83% of C++ online submissions for Valid Anagram.
Memory Usage: 9.6 MB, less than 55.22% of C++ online submissions for Valid Anagram.


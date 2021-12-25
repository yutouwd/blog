---
title: 387.First Unique Character in a String
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
abbrlink: 1245254830
date: 2019-08-29 17:07:56
---
# 题目描述
Given a string, find the first non-repeating character in it and return it's index. If it doesn't exist, return -1.

Examples:

s = "leetcode"
return 0.

s = "loveleetcode",
return 2.
Note: You may assume the string contain only lowercase letters.
# 我的解法
## 解题思路
题目要求判断一个字符串中第一个不重复的字符，可以用一个map来统计字符串中字符出现的次数，然后再找到第一个出现次数为1的字符就可以了
## 实现代码
```C++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, int> chara;
        for (char i : s) chara[i]++;
        for (int i = 0; i < s.size(); i++){
            if (chara[s[i]] == 1)
                return i;
        }
        return -1;
    }
};
```
Runtime: 52 ms, faster than 59.91% of C++ online submissions for First Unique Character in a String.
Memory Usage: 12.9 MB, less than 68.75% of C++ online submissions for First Unique Character in a String.

# 高票解法
用时稍微有些长，因为要遍历字符串两遍，如果字符串很长就要用时很久，看到一个只用遍历一变的方法，就是第一次遍历的时候同时也要储存字符的位置，然后之后直接遍历map找到出现一次且位置最前的字符就可以了。
## 实现代码
```C++
class Solution {
public:
    int firstUniqChar(string s) {
        unordered_map<char, pair<int, int>> m;
        int idx = s.size();
        for (int i = 0; i < s.size(); i++) {
            m[s[i]].first++;
            m[s[i]].second = i;
        }
        for (auto &p : m) {
            if (p.second.first == 1) idx = min(idx, p.second.second);
        }
        return idx == s.size() ? -1 : idx;
    }
};

```

Runtime: 68 ms, faster than 31.77% of C++ online submissions for First Unique Character in a String.
Memory Usage: 13.3 MB, less than 10.94% of C++ online submissions for First Unique Character in a String.

用时好像还更久一点。。。


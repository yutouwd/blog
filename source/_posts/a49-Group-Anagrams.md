---
title: 49.Group Anagrams
tags:
  - leetcode
  - hashmap
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 3379987828
date: 2020-12-14 14:16:37
---
# 题目描述
Given an array of strings strs, group the anagrams together. You can return the answer in any order.

An Anagram is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.


Example 1:
Input: strs = ["eat","tea","tan","ate","nat","bat"]
Output: [["bat"],["nat","tan"],["ate","eat","tea"]]

Example 2:
Input: strs = [""]
Output: [[""]]

Example 3:
Input: strs = ["a"]
Output: [["a"]]
 

Constraints:

1 <= strs.length <= 104
0 <= strs[i].length <= 100
strs[i] consists of lower-case English letters.

# 我的解法
## 解题思路
不太会做的一题，看了下题解，可以用hashmap来存放整个字符串数组，key是经过排序的string，value是一个字符串数组，包含来所有当前字母组合的字符串。
## 实现代码
```C++
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        unordered_map<string, vector<string>> m;
        for (const auto& str : strs){
            auto key = str;
            sort(key.begin(), key.end());
            m[key].push_back(str);
        }        
        for (const auto& im : m)
            res.push_back(im.second);
        return res;
    }
};
```

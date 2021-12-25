---
title: 567.Permutation in String
tags:
  - leetcode
  - 滑动窗口
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 3971953535
date: 2021-07-27 22:55:19
---
# 题目描述
给定两个字符串 s1 和 s2，写一个函数来判断 s2 是否包含 s1 的排列。

换句话说，第一个字符串的排列之一是第二个字符串的 子串 。 

示例 1：
输入: s1 = "ab" s2 = "eidbaooo"
输出: True
解释: s2 包含 s1 的排列之一 ("ba").

示例 2：
输入: s1= "ab" s2 = "eidboaoo"
输出: False
 

提示：
1 <= s1.length, s2.length <= 104
s1 和 s2 仅包含小写字母

# 我的解法
## 解题思路
判断字符串二中是否有和字符串中一样的排列（有相同的字符和他们的数量）。使用滑动窗口，记录字符串二窗口中的各个字符数。如果字符只有小写的话，使用数组会方便些。
## 实现代码
```C++
class Solution {
public:
    bool checkInclusion(string s1, string s2) {
        int n1 = s1.size(), n2 = s2.size();
        if (n1 > n2) return false;
        
        vector<int> v1(26, 0);
        vector<int> v2(26, 0);

        for (int i = 0; i < n1; i++){
            v1[(s1[i] - 'a')]++;
            v2[(s2[i] - 'a')]++;
        }
        if (v1 == v2) return true;
        for (int i = n1; i < n2; i++){
            v2[(s2[i-n1] - 'a')]--;
            v2[(s2[i] - 'a')]++;
            if (v1 == v2) return true;
        }
        return false;
    }
};
```

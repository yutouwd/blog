---
title: 771.Jewels and Stones
tags:
  - leetcode
  - hashmap
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 2189086012
date: 2020-10-02 22:46:17
---
# 题目描述
You're given strings J representing the types of stones that are jewels, and S representing the stones you have.  Each character in S is a type of stone you have.  You want to know how many of the stones you have are also jewels.

The letters in J are guaranteed distinct, and all characters in J and S are letters. Letters are case sensitive, so "a" is considered a different type of stone from "A".

Example 1:
Input: J = "aA", S = "aAAbbbb"
Output: 3

Example 2:
Input: J = "z", S = "ZZ"
Output: 0
Note:

S and J will consist of letters and have length at most 50.
The characters in J are distinct.


# 我的解法
## 解题思路
这题比较简单，使用一个map来记录S中字符出现的次数，然后再在map里查找有没有J中的字符出现。
## 实现代码
```C++
class Solution {
public:
    int numJewelsInStones(string J, string S) {
        unordered_map<char, int> m;
        for (char c : S)
            m[c]++;
        int res = 0;
        for (char c : J){
            if (m.find(c) != m.end())
                res += m[c];
        }
        return res;
    }
};
```

执行用时：4 ms, 在所有 C++ 提交中击败了67.30%的用户
内存消耗：6.2 MB, 在所有 C++ 提交中击败了56.14%的用户
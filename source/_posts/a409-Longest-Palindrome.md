---
title: 409.Longest Palindrome
tags:
  - leetcode
  - hashmap
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 2988636715
date: 2020-12-14 18:57:24
---
# 题目描述
Given a string s which consists of lowercase or uppercase letters, return the length of the longest palindrome that can be built with those letters.

Letters are case sensitive, for example, "Aa" is not considered a palindrome here.

 

Example 1:

Input: s = "abccccdd"
Output: 7
Explanation:
One longest palindrome that can be built is "dccaccd", whose length is 7.
Example 2:

Input: s = "a"
Output: 1
Example 3:

Input: s = "bb"
Output: 2
 

Constraints:

1 <= s.length <= 2000
s consits of lower-case and/or upper-case English letters only.

# 我的解法
## 解题思路
给一个字符串，根据字符串里面的字符来构造一个最长的回文串，返回最长回文串的长度。

先用一个map来记录每个字符出现的次数，然后出现偶数次的字符都可以取，如果出现次数为奇数，那么只能取他的出现次数减一。最后在判断有没有出现次数为奇数的，有的话就加一。
## 实现代码
```C++
class Solution {
public:
    int longestPalindrome(string s) {
        unordered_map<char, int> m;
        for (char c : s)
            m[c]++;
        int res = 0;
        bool flag = false;
        for (auto p : m){
            res += p.second / 2 * 2;
            if (p.second % 2 == 1)
                flag = true;
        }
        res += flag;
        return res;
    }
};
```

执行用时：4 ms, 在所有 C++ 提交中击败了87.78%的用户
内存消耗：7 MB, 在所有 C++ 提交中击败了14.58%的用户
---
title: 3.Longest Substring without Repeating Characters
tags:
  - leetcode
  - hashmap
  - 滑动窗口
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 1224454559
date: 2021-07-27 22:20:29
---
# 题目描述
Given a string s, find the length of the longest substring without repeating characters.

Example 1:
Input: s = "abcabcbb"
Output: 3
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: s = "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:
Input: s = "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3.
Notice that the answer must be a substring, "pwke" is a subsequence and not a substring.

Example 4:
Input: s = ""
Output: 0
 
Constraints:
0 <= s.length <= 5 * 104
s consists of English letters, digits, symbols and spaces.


# 我的解法
## 解题思路
找到字符串的最长无重复字符的子串。使用滑动窗口来记录当前字串存在的字符，及其数量。如果当前没有重复的字符，那么后指针就往后移动，如果有，那么就将前指针往后移动。
## 实现代码

```C++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        int n = s.size();
        if (n < 2) return n;
        int i = 0, j = 1;
        unordered_map<char, int> m;
        m[s[0]]++;
        int maxLen = 1, curLen = 1;
        while (i < n-1){
            if (m.find(s[j]) != m.end() && m[s[j]] >= 1){
                m[s[i++]]--;
                curLen--;
                continue;
            }
            else if (j < n){
                m[s[j++]]++;
                curLen++;
            }
            if (curLen > maxLen)
                maxLen = curLen;
            if (j == n)
                break;
        }

        return maxLen;
    }
};
```


---
title: 1160.Find Words That Can Be Formed by Characters
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 3557020099
date: 2020-03-23 19:36:50
---
# 题目描述
You are given an array of strings words and a string chars.

A string is good if it can be formed by characters from chars (each character can only be used once).

Return the sum of lengths of all good strings in words.

Example 1:
Input: words = ["cat","bt","hat","tree"], chars = "atach"
Output: 6
Explanation: 
The strings that can be formed are "cat" and "hat" so the answer is 3 + 3 = 6.

Example 2:
Input: words = ["hello","world","leetcode"], chars = "welldonehoneyr"
Output: 10
Explanation: 
The strings that can be formed are "hello" and "world" so the answer is 5 + 5 = 10.
 
Note:
1 <= words.length <= 1000
1 <= words[i].length, chars.length <= 100
All strings contain lowercase English letters only.

# 我的解法
## 实现代码
题目要求是在字母表中的字符能不能拼出词汇表中的某一个单词。

```C++

class Solution {
public:
    int countCharacters(vector<string>& words, string chars) {
        unordered_map<char, int> m;
        for (char c : chars)
            m[c]++;
        int ans = 0;
        for (string s : words){
            bool is_spell = true;
            unordered_map<char, int> tmp;
            for (char c : s)
                tmp[c]++;
            for (char c : s){
                if (m[c] < tmp[c]){
                    is_spell = false;
                    break;
                }
            }
            if (is_spell)
                ans += s.size();
        }
        return ans;
    }
};
```

Runtime: 352 ms, faster than 5.25% of C++ online submissions for Find Words That Can Be Formed by Characters.
Memory Usage: 54.5 MB, less than 100.00% of C++ online submissions for Find Words That Can Be Formed by Characters.
---
title: 844.Backspace String Compare
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 3938366888
date: 2020-10-20 00:00:45
---
# 题目描述
Given two strings S and T, return if they are equal when both are typed into empty text editors. # means a backspace character.

Note that after backspacing an empty text, the text will continue empty.

Example 1:

Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
Example 2:

Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
Example 3:

Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
Example 4:

Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
Note:

1 <= S.length <= 200
1 <= T.length <= 200
S and T only contain lowercase letters and '#' characters.
Follow up:

Can you solve it in O(N) time and O(1) space?


# 我的解法
## 实现代码

```C++
class Solution {
public:
    string backspace(string s){
        string res;
        for (char c : s){
            if (c != '#')
                res += c;
            else if (c == '#'){
                res = res.substr(0,res.size()-1);
            }
        }
        return res;
    }
    bool backspaceCompare(string S, string T) {
        return backspace(S) == backspace(T);
    }
};
```
执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
内存消耗：6.4 MB, 在所有 C++ 提交中击败了35.40%的用户
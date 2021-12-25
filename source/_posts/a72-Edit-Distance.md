---
title: 72.Edit Distance
tags:
  - leetcode
  - 动态规划
categories:
  - leetcode
  - hard
copyright: true
comments: true
abbrlink: 3404414355
date: 2021-01-22 09:17:32
---
# 题目描述
Given two strings word1 and word2, return the minimum number of operations required to convert word1 to word2.

You have the following three operations permitted on a word:

Insert a character
Delete a character
Replace a character
 

Example 1:
Input: word1 = "horse", word2 = "ros"
Output: 3
Explanation: 
horse -> rorse (replace 'h' with 'r')
rorse -> rose (remove 'r')
rose -> ros (remove 'e')

Example 2:
Input: word1 = "intention", word2 = "execution"
Output: 5
Explanation: 
intention -> inention (remove 't')
inention -> enention (replace 'i' with 'e')
enention -> exention (replace 'n' with 'x')
exention -> exection (replace 'n' with 'c')
exection -> execution (insert 'u')


# 我的解法
## 解题思路
没想到面试里上来就来了一道hard题目，好在在提示下写出来了差不多。最主要就是状态转移方程代表的意义，dp\[i\]\[j\]代表的是word1前i位转换为word2前j位需要最少的步骤。
## 实现代码
```C++
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.length();
        int m = word2.length();
        if (n == 0) return m;
        if (m == 0) return n;
        vector<vector<int>> dp(n+1, vector<int> (m+1,0));
        for (int i = 0; i < n+1; i++)
            dp[i][0] = i;
        for (int j = 0; j < m+1; j++)
            dp[0][j] = j;
        for (int i = 1; i < n+1; i++){
            for (int j = 1; j < m+1; j++){
                if (word1[i-1] == word2[j-1]){
                    dp[i][j] = min(dp[i-1][j-1],min(dp[i-1][j]+1,dp[i][j-1]+1));
                }
                else{
                    dp[i][j] = min(dp[i-1][j-1]+1, min(dp[i-1][j]+1, dp[i][j-1]+1));
                }
            }
        }
        return dp[n][m];
    }
};
```


# 583. Delete Operation for Two Strings
Given two strings word1 and word2, return the minimum number of steps required to make word1 and word2 the same.
In one step, you can delete exactly one character in either string.

 

Example 1:
Input: word1 = "sea", word2 = "eat"
Output: 2
Explanation: You need one step to make "sea" to "ea" and another step to make "eat" to "ea".

Example 2:
Input: word1 = "leetcode", word2 = "etco"
Output: 4
 
Constraints:
1 <= word1.length, word2.length <= 500
word1 and word2 consist of only lowercase English letters.

## 解题思路
这题其实是编辑距离更简单的版本，没有了插入和替换，但是做每日一题的时候还是想不出来怎么做。

```C++
class Solution {
public:
    int minDistance(string word1, string word2) {
        int n = word1.size(), m = word2.size();
        vector<vector<int>> dp(n+1, vector<int>(m+1,0));
        for (int i = 1; i <= n; i++)
            dp[i][0] = i;
        for (int j = 1; j <= m; j++)
            dp[0][j] = j;
        for (int i = 1; i <= n; i++){
            char a = word1[i-1];
            for (int j = 1; j <= m; j++){
                char b = word2[j-1];
                if (a == b)
                    dp[i][j] = dp[i-1][j-1];
                else
                    dp[i][j] = min(dp[i-1][j], dp[i][j-1]) + 1;
            }
        }
        return dp[n][m];
    }
};
```
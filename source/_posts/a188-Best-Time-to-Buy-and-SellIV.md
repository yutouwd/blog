---
title: 188.Best Time to Buy and Sell IV
tags:
  - leetcode
  - 动态规划
categories:
  - leetcode
  - hard
copyright: true
comments: true
abbrlink: 1646362365
date: 2020-02-26 18:52:14
---
# 题目描述

# 我的解法
## 解题思路
直接使用[#123][1]的方法会超时，是因为k有时会取非常大的情况，这就导致dp数组非常大，要遍历的情况就太多了。所以可以将k>n/2的时候将问题退化成k等于无穷的情况，减少运算量就可以避免过高的运算量了。

## 实现代码
```C++
class Solution {
public:
    int maxProfitInfK(vector<int>& prices){
        int dp_i_0 = 0, dp_i_1 = INT_MIN;
        for (int i = 0; i < prices.size(); i++){
            int tmp = dp_i_0;
            dp_i_0 = max(dp_i_0, dp_i_1 + prices[i]);
            dp_i_1 = max(dp_i_1, tmp - prices[i]);
        }
        return dp_i_0;
    }
    int maxProfit(int k, vector<int>& prices) {
        // 初始化三维dp数组
        int n = prices.size();
        if (k > n/2){
            return maxProfitInfK(prices);
        }
        else{
            vector<vector<vector<int>>> dp(n+1, vector<vector<int>>(k+1,vector<int>(2,0)));
            // base case
            for (int j = 0; j < k + 1; j++)
                dp[0][j][1] = INT_MIN;
            for (int i = 0; i < n + 1; i++)
                dp[i][0][1] = INT_MIN;
            for (int i = 1; i < n + 1; i++){
                for (int j = k; j > 0; j--){
                    dp[i][j][0] = max(dp[i-1][j][0], dp[i-1][j][1] + prices[i-1]);
                    dp[i][j][1] = max(dp[i-1][j][1], dp[i-1][j-1][0] - prices[i-1]);
                }
            }
            return dp[n][k][0];
        }
    }
};
```
Runtime: 32 ms, faster than 31.43% of C++ online submissions for Best Time to Buy and Sell Stock IV.
Memory Usage: 19.5 MB, less than 5.55% of C++ online submissions for Best Time to Buy and Sell Stock IV.

[1]:https://yutouwd.github.io/posts/974687170

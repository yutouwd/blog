---
title: 309.Best Time to Buy and Sell with Cooldown
tags:
  - leetcode
  - 动态规划
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 4032611973
date: 2020-02-27 20:07:41
---
# 题目描述
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times) with the following restrictions:

You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
After you sell your stock, you cannot buy stock on next day. (ie, cooldown 1 day)

Example:
Input: [1,2,3,0,2]
Output: 3 
Explanation: transactions = [buy, sell, cooldown, buy, sell]


# 我的解法
## 实现代码
```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        
        // base case
        int dp_i_0 = 0;
        int dp_i_1 = INT_MIN;
        int dp_pre = 0;
        // dp
        for (int i = 0; i < n; i++){
            int tmp = dp_i_0;
            dp_i_0 = max(dp_i_0, dp_i_1 + prices[i]);
            dp_i_1 = max(dp_i_1, dp_pre - prices[i]);
            dp_pre = tmp;
        }
        return dp_i_0;
        
    }
};
```


---
title: 122.Best Time to Buy and Sell Stock II
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 473611493
date: 2019-09-20 15:54:43
---
# 题目描述
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (i.e., buy one and sell one share of the stock multiple times).

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:
Input: [7,1,5,3,6,4]
Output: 7
Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.
             Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.

Example 2:
Input: [1,2,3,4,5]
Output: 4
Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.
             Note that you cannot buy on day 1, buy on day 2 and sell them later, as you are
             engaging multiple transactions at the same time. You must sell before buying again.

Example 3:
Input: [7,6,4,3,1]
Output: 0
Explanation: In this case, no transaction is done, i.e. max profit = 0.

# 我的解法
## 解题思路
可以使用一种投机的方法，只要第二天的股价大于第一天，就可以在第一天买入，在第二天卖出，因为一定会有收益
## 实现代码
```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if (prices.size() <= 1) return 0;
        int profit = 0;
        for (int i = 0; i < prices.size() - 1; i++){
            if (prices[i] < prices[i+1])
                profit += prices[i+1] - prices[i];
        }
        return profit;
    }
};
```

Runtime: 4 ms, faster than 98.15% of C++ online submissions for Best Time to Buy and Sell Stock II.
Memory Usage: 9.6 MB, less than 68.25% of C++ online submissions for Best Time to Buy and Sell Stock II.


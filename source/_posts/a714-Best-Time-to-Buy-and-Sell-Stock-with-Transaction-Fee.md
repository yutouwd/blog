---
title: 714.Best Time to Buy and Sell Stock with Transaction Fee
tags:
  - leetcode
  - 动态规划
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 1342612877
date: 2020-12-17 12:29:11
---
# 题目描述
Your are given an array of integers prices, for which the i-th element is the price of a given stock on day i; and a non-negative integer fee representing a transaction fee.

You may complete as many transactions as you like, but you need to pay the transaction fee for each transaction. You may not buy more than 1 share of a stock at a time (ie. you must sell the stock share before you buy again.)

Return the maximum profit you can make.

Example 1:
Input: prices = [1, 3, 2, 8, 4, 9], fee = 2
Output: 8
Explanation: The maximum profit can be achieved by:
Buying at prices[0] = 1
Selling at prices[3] = 8
Buying at prices[4] = 4
Selling at prices[5] = 9
The total profit is ((8 - 1) - 2) + ((9 - 4) - 2) = 8.
Note:

0 < prices.length <= 50000.
0 < prices[i] < 50000.

# 我的解法
## 解题思路
动态规划：状态为当前的利润，分为当前持有和不持有两种情况。
## 实现代码
```C++
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        vector<int> dp_0 (n, 0); // 未持有
        vector<int> dp_1 (n, 0); // 持有
        dp_1[0] = -prices[0];         
        for (int i = 1; i < n; i++){
            dp_0[i] = max(dp_0[i-1], dp_1[i-1]+prices[i]-fee);
            dp_1[i] = max(dp_1[i-1], dp_0[i-1]-prices[i]);
            
        }
        return dp_0[n-1];
    }
};
```

执行用时：208 ms, 在所有 C++ 提交中击败了80.02%的用户
内存消耗：55.4 MB, 在所有 C++ 提交中击败了28.21%的用户

可以不用数组来做
```C++
class Solution {
public:
    int maxProfit(vector<int>& prices, int fee) {
        int n = prices.size();
        int dp0 = 0, dp1 = -prices[0];       
        for (int i = 1; i < n; i++){
            int tmp = dp0;
            dp0 = max(dp0, dp1+prices[i]-fee);
            dp1 = max(dp1, tmp-prices[i]);
        }
        return dp0;
    }
};
```

执行用时：204 ms, 在所有 C++ 提交中击败了84.78%的用户
内存消耗：50.9 MB, 在所有 C++ 提交中击败了65.83%的用户
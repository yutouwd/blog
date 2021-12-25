---
title: 123.Best Time to Buy and Sell III
tags:
  - leetcode
  - math
  - 动态规划
categories:
  - leetcode
  - hard
copyright: true
comments: true
notshow: true
abbrlink: 974687170
date: 2019-09-21 22:22:19
---
# 题目描述
Say you have an array for which the ith element is the price of a given stock on day i.
Design an algorithm to find the maximum profit. You may complete at most two transactions.

Note: You may not engage in multiple transactions at the same time (i.e., you must sell the stock before you buy again).

Example 1:
Input: [3,3,5,0,0,3,1,4]
Output: 6
Explanation: Buy on day 4 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
             Then buy on day 7 (price = 1) and sell on day 8 (price = 4), profit = 4-1 = 3.

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
也在面试的时候遇到了这道题，后悔没有把这一系列的题目做完。现在再做的话还是做不出来😂。

终于终于在7个月之后开始做完了这道题，当然做还是不会做的😂，主要参考了：<https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-iii/solution/yi-ge-tong-yong-fang-fa-tuan-mie-6-dao-gu-piao-wen/>



## 思路分析
思路是穷举出所有的可能，那么一共有3个状态：第一个是天数；第二个是允许交易的最大次数；第三个是当前的持有状态。于是用一个三位的数组就可以穷举出所有可能了。例如：

> dp\[3\]\[2\]\[1]的含义就是：今天是第三天，我现在手上持有着股票，至今最多进行2次交易。再比如dp\[2\]\[3\]\[0\] 的含义：今天是第二天，我现在手上没有持有股票，至今最多进行3次交易。


这样最终的最大利润就是dp\[n-1\]\[k\]\[0\]，n-1代表这最后一天；0代表当前不持有股票，因为股票卖出去肯定比不卖出去的利润要大；不过最不好理解的就k了，一开始觉得为什么k这里不应该是0呢？因为k代表着交易的次数，如果还是k的话不就是一次也没有交易吗？后来想了想才理解了比如说dp\[10\]\[2\]\[0]代表这第十天最多买卖两次，dp\[10\]\[1\]\[0]则代表着最多买卖1次，很明显多一次买卖的机会可能获得的最大利润要比只有一次的多，所以最大利润应该是在k次这里取得。

然后就是状态转移方程的分析了：

```C++
dp[i][k][0] = max(dp[i-1][k][0], dp[i-1][k][1] + prices[i])
// 代表着今天不持有股票，那么可能是昨天也没有持有股票，或者是昨天持有今天卖出去了。

dp[i][k][1] = max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i])
//代表今天持有股票，可能是昨天持有今天不变，或者昨天未持有今天买入
```

这里第二个式子的k也同样有点难以理解，一开始不明白为什么是前一天的k要减一，其实是因为如果要今天买入股票，那么肯定要占用一次名额，那么昨天最多能进行买卖的名额就少了1。

状态转移方程有了，剩下的就是要考虑下一些base case了，就是一些简单的情况要初始化好：
```C++
dp[-1][k][0] = 0
//解释：因为 i 是从 0 开始的，所以 i = -1 意味着还没有开始，这时候的利润当然是 0 。
dp[-1][k][1] = -infinity
//解释：还没开始的时候，是不可能持有股票的，用负无穷表示这种不可能。
dp[i][0][0] = 0
//解释：因为 k 是从 1 开始的，所以 k = 0 意味着根本不允许交易，这时候利润当然是 0 。
dp[i][0][1] = -infinity
//解释：不允许交易的情况下，是不可能持有股票的，用负无穷表示这种不可能。
```
因为C++中数组不能有-1的索引，所以在算法实现的时候将0设置成这里的-1，而1是真正的第一天。

## 实现代码
```C++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        // 初始化一个三维数组，初始化为0
        int n = prices.size();
        vector<vector<vector<int>>> dp(n+1, vector<vector<int>>(3, vector<int>(2,0)));
        // base case的初始化
        dp[0][2][1] = INT_MIN;
        dp[0][1][1] = INT_MIN;
        for (int i = 0; i < n+1; i++){
            dp[i][0][1] = INT_MIN;
        }
        // 状态转移方程，穷举所有的可能
        for (int i = 1; i < n+1; i++){
            for (int k = 2; k > 0; k--){
                dp[i][k][0] = max(dp[i-1][k][0], dp[i-1][k][1] + prices[i-1]);
                dp[i][k][1] = max(dp[i-1][k][1], dp[i-1][k-1][0] - prices[i-1]);
                
            }
        }
        // 返回第n天，最多买卖2次，不持有股票的最大利润
        return dp[n][2][0];
    }
};
```
Runtime: 28 ms, faster than 9.85% of C++ online submissions for Best Time to Buy and Sell Stock III.
Memory Usage: 18.2 MB, less than 7.14% of C++ online submissions for Best Time to Buy and Sell Stock III.
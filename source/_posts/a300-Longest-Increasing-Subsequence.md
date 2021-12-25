---
title: 300.Longest Increasing Subsequence
tags:
  - leetcode
  - 动态规划
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 2008457831
date: 2020-03-23 19:29:11
---
# 题目描述
Given an unsorted array of integers, find the length of longest increasing subsequence.

Example:
Input: [10,9,2,5,3,7,101,18]
Output: 4 
Explanation: The longest increasing subsequence is [2,3,7,101], therefore the length is 4. 
Note:

There may be more than one LIS combination, it is only necessary for you to return the length.
Your algorithm should run in O(n2) complexity.
Follow up: Could you improve it to O(n log n) time complexity?

# 我的解法
## 解题思路
用动态规划，状态转移方程应该为：
如果nums[i]>nums[j] (i>j)
dp[i] = max(dp[i], dp[j]+1)
最后的解就是dp数组中的最大值。
## 实现代码
```C++
class Solution {
public:
    int lengthOfLIS(vector<int>& nums) {
        if (nums.size() == 0) return 0;
        vector<int> dp(nums.size(), 1);
        for (int i = 1; i < nums.size(); i++){
            for (int j = 0; j < i; j++){
                if (nums[i] > nums[j])
                    dp[i] = max(dp[j] + 1, dp[i]);
            }
        }
        return *max_element(dp.begin(), dp.end());
    }
};
```
Runtime: 76 ms, faster than 8.02% of C++ online submissions for Longest Increasing Subsequence.
Memory Usage: 6.5 MB, less than 100.00% of C++ online submissions for Longest Increasing Subsequence.



# 673. Number of Longest Increasing-Subsequence

基于300题的进阶题目，要求求出最长的递增子串并且求出数量。看了答案才做出来。除了dp数组以外，还需要维护一个cnt数组，来记录当前长度子串的数量。


```C++
class Solution {
public:
    int findNumberOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n, 1);
        vector<int> cnt(n, 1);
        int maxLen = 0, ans = 0;
        for (int i = 0; i < n; i++){
            for (int j = 0; j < i; j++){
                if (nums[i] > nums[j]){
                    if (dp[j] + 1 > dp[i]){
                        dp[i] = dp[j] + 1;
                        cnt[i] = cnt[j];
                    }
                    else if (dp[j] + 1 == dp[i]){
                        cnt[i] += cnt[j];
                    }
                }
            }

            if (dp[i] > maxLen){
                maxLen = dp[i];
                ans = cnt[i];
            }
            else if (dp[i] == maxLen){
                ans += cnt[i];
            }
        }
        return ans;
    }
};
```
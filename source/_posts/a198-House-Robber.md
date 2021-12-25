---
title: 198.House Robber
tags:
  - leetcode
  - 动态规划
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2797751844
date: 2019-09-25 13:31:57
---
# 题目描述
You are a professional robber planning to rob houses along a street. Each house has a certain amount of money stashed, the only constraint stopping you from robbing each of them is that adjacent houses have security system connected and it will automatically contact the police if two adjacent houses were broken into on the same night.

Given a list of non-negative integers representing the amount of money of each house, determine the maximum amount of money you can rob tonight without alerting the police.

Example 1:
Input: [1,2,3,1]
Output: 4
Explanation: Rob house 1 (money = 1) and then rob house 3 (money = 3).
             Total amount you can rob = 1 + 3 = 4.

Example 2:
Input: [2,7,9,3,1]
Output: 12
Explanation: Rob house 1 (money = 2), rob house 3 (money = 9) and rob house 5 (money = 1).
             Total amount you can rob = 2 + 9 + 1 = 12.

# 我的解法
## 解题思路
感觉和最大子集有点类似，可以用动态规划的方法。

1. 当n等于1时，只能抢第一个房子。
2. 当n等于2时，这时候抢两个房子中最大的max(n1,n2)。
3. 当n等于3时，如果就要抢max(n1+n3,n2)
## 实现代码
```C++
class Solution {
public:
    int rob(vector<int>& nums) {
        if (nums.size() <= 0) return 0;
        if (nums.size() == 1) return nums[0];
        if (nums.size() == 2) return max(nums[0],nums[1]);
        vector<int> dp(nums.size(), 0);
        dp[0] = nums[0];
        dp[1] = max(nums[0], nums[1]);
        for (int i = 2; i < nums.size(); i++){
            dp[i] = max(dp[i-2] + nums[i], dp[i-1]);
        }
        return dp[nums.size() - 1];
    }
};
```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for House Robber.
Memory Usage: 8.5 MB, less than 92.45% of C++ online submissions for House Robber.



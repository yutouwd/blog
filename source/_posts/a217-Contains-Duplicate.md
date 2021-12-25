---
title: 217.Contains Duplicate
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 679636703
date: 2019-07-21 11:00:48
---
# 题目描述
Given an array of integers, find if the array contains any duplicates.

Your function should return true if any value appears at least twice in the array, and it should return false if every element is distinct.

Example 1:
Input: [1,2,3,1]
Output: true

Example 2:
Input: [1,2,3,4]
Output: false

Example 3:
Input: [1,1,1,3,3,4,3,2,4,2]
Output: true

# 我的解法
## 解题思路
题目要求判断一个数组里面有没有重复的数字，最先想到的办法当然是暴力法，就把数组里全部的数字都比较一遍，如果有重复就返回true，没有就返回false
## 实现代码
```C++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++){
            for (int j = i+1; j < nums.size(); j++){
                if (nums[i] == nums[j])
                    return true;
            }
        }
        return false;
    }
};
```
但是发现会超出时间限制。
# 高票解法
高票解法中用了set，只用1行就可以了。或者可以用sort函数先将数组进行排序，然后排序后如果有重复的数字一定会在相邻的位置。
## 实现代码
```C++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        return nums.size() > set<int>(nums.begin(),nums.end()).size();
    }
};
```
Runtime: 52 ms, faster than 29.45% of C++ online submissions for Contains Duplicate.
Memory Usage: 18.1 MB, less than 5.06% of C++ online submissions for Contains 

```C++
class Solution {
public:
    bool containsDuplicate(vector<int>& nums) {
        if (nums.size() == 0)
            return false;
        sort(nums.begin(),nums.end());
        for (int i = 0; i < nums.size()-1; i++)
            if (nums[i] == nums[i+1])
                return true;
        return false;
    }
};
```
Runtime: 24 ms, faster than 99.01% of C++ online submissions for Contains Duplicate.
Memory Usage: 11.2 MB, less than 95.37% of C++ online submissions for Contains Duplicate.
# 知识总结
学习C++中set和sort的用法
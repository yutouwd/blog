---
title: 169.Majority Element
tags:
  - leetcode
categories:
  - leetcode
copyright: true
comments: true
notshow: true
abbrlink: 3720766983
date: 2019-10-17 14:08:13
---
# 题目描述
Given an array of size n, find the majority element. The majority element is the element that appears more than ⌊ n/2 ⌋ times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example 1:
Input: [3,2,3]
Output: 3

Example 2:
Input: [2,2,1,1,1,2,2]
Output: 2
# 我的解法
## 解题思路
按照分治法的标签找到的题目，但是感觉可以直接用一个map来记录每个数字出现的次数，然后再遍历map找到出现最多的次数就可以了。
## 实现代码
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int, int> count;
        for (int i : nums)
            count[i]++;
        int maxNum = 0;
        int maxCount = 0;
        for (auto i : count){
            if (i.second > maxCount){
                maxCount = i.second;
                maxNum = i.first;
            }
        }
        return maxNum;
    }
};
```
Runtime: 20 ms, faster than 77.92% of C++ online submissions for Majority Element.
Memory Usage: 11.2 MB, less than 48.48% of C++ online submissions for Majority Element.

# 高票解法
在讨论区看到了一个更加简洁的方法，在统计的同时进行判断，如果大于数组的长度的二分之一就一定是众数了。
## 实现代码
```C++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        unordered_map<int, int> counter;
        for (int num : nums){
            if (++counter[num] > nums.size() / 2)
                return num;
        }
        return 0;
    }
};
```


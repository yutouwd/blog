---
title: 350.Intersection of Two Arrays II
tags:
  - leetcode
  - vector
  - hashmap
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2444108763
date: 2019-12-11 22:37:05
---
# 题目描述
Given two arrays, write a function to compute their intersection.

Example 1:
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2,2]

Example 2:
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [4,9]

Note:
Each element in the result should appear as many times as it shows in both arrays.
The result can be in any order.

Follow up:
What if the given array is already sorted? How would you optimize your algorithm?
What if nums1's size is small compared to nums2's size? Which algorithm is better?
What if elements of nums2 are stored on disk, and the memory is limited such that you cannot load all elements into the memory at once?
# 我的解法
## 解题思路
统计两个数组重复的数字，如果一个数字在两个数组中都出现了2次，那么返回数组也要包括两个这个数组。还是用unordered_map来实现，统计第一个数组每个数字出现的次数，然后再遍历第二个数组，如果有重复的数字，那么就加到答案数组中，并且将map中的key值减1。
## 实现代码
```C++
class Solution {
public:
    vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> count;
        for (int i : nums1)
            count[i]++;
        vector<int> ans;
        for (int i : nums2){
            if (count[i]){
                ans.push_back(i);
                count[i]--;
            }
        }
        return ans;
    }
};
```
Runtime: 4 ms, faster than 99.18% of C++ online submissions for Intersection of Two Arrays II.
Memory Usage: 9.7 MB, less than 26.79% of C++ online submissions for Intersection of Two Arrays II.

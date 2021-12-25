---
title: 88.Merge Sorted Array
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 1685248582
date: 2020-01-06 23:21:28
---
# 题目描述
Given two sorted integer arrays nums1 and nums2, merge nums2 into nums1 as one sorted array.

Note:

The number of elements initialized in nums1 and nums2 are m and n respectively.
You may assume that nums1 has enough space (size that is greater or equal to m + n) to hold additional elements from nums2.
Example:

Input:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

Output: [1,2,2,3,5,6]
# 我的解法
## 解题思路
从nums1和nums2有数字的最后开始比较大小，将大的放到nums1的最后。
## 实现代码
```C++
class Solution {
public:
    void merge(vector<int>& nums1, int m, vector<int>& nums2, int n) {
        if (n == 0) return;
        int i = m + n -1, j = m - 1, k = n - 1;
        while(j >= 0  && k >= 0){
            if (nums1[j] > nums2[k]){
                nums1[i] = nums1[j];
                j--;
            }
            else{
                nums1[i] = nums2[k];
                k--;
            }
            i--;
        }
        if (k >= 0 && j <= 0){
            while(k >= 0){
                nums1[i--] = nums2[k--];
            }  
        }
    }
};
```

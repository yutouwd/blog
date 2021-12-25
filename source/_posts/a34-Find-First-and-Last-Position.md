---
title: 34.Find First and Last Position of Element in Sorted Array
tags:
  - leetcode
  - 二分查找
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 932931314
date: 2021-08-23 12:14:28
---
# 题目描述
给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。
如果数组中不存在目标值 target，返回 [-1, -1]。

进阶：
你可以设计并实现时间复杂度为 O(log n) 的算法解决此问题吗？
 

示例 1：
输入：nums = [5,7,7,8,8,10], target = 8
输出：[3,4]

示例 2：
输入：nums = [5,7,7,8,8,10], target = 6
输出：[-1,-1]

示例 3：
输入：nums = [], target = 0
输出：[-1,-1]

## 解题思路
用二分查找找到目标数的位置，然后再向前和向后找到它的范围。
## 实现代码
```C++
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        int n = nums.size();
        int low = 0, upp = n-1;
        int mid = 0;
        bool finded = false;
        while (low <= upp){
            mid = (low + upp) / 2;
            if (nums[mid] == target){
                finded = true;
                break;
            }
            else if (nums[mid] < target)
                low = mid + 1;
            else
                upp = mid - 1;
        }
        if (finded){
            low = mid;
            upp = mid;
            while(low >= 0 && nums[low] == target)
                low--;
            while(upp < n && nums[upp] == target)
                upp++;
            return {low+1, upp-1};
        }
        else
            return {-1,-1};
    }
};
```

## 优化一下
但是仔细一想，之前找目标数的范围最坏情况下时间复杂度是O(n)了。看了下题解，可以用二分法来找到第一个大于或小于目标数的位置。
```C++
class Solution { 
public:
    int binarySearch(vector<int>& nums, int target, bool lower) {
        int left = 0, right = (int)nums.size() - 1, ans = (int)nums.size();
        while (left <= right) {
            int mid = (left + right) / 2;
            if (nums[mid] > target || (lower && nums[mid] >= target)) {
                right = mid - 1;
                ans = mid;
            } else {
                left = mid + 1;
            }
        }
        return ans;
    }

    vector<int> searchRange(vector<int>& nums, int target) {
        int leftIdx = binarySearch(nums, target, true);
        int rightIdx = binarySearch(nums, target, false) - 1;
        if (leftIdx <= rightIdx && rightIdx < nums.size() && nums[leftIdx] == target && nums[rightIdx] == target) {
            return vector<int>{leftIdx, rightIdx};
        } 
        return vector<int>{-1, -1};
    }
};

```

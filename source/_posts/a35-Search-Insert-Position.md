---
title: 35.Search Insert Position
tags:
  - leetcode
  - vector
  - 二分查找
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 1764221558
date: 2020-09-03 12:57:25
---
# 题目描述
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

示例 1:
输入: [1,3,5,6], 5
输出: 2

示例 2:
输入: [1,3,5,6], 2
输出: 1

示例 3:
输入: [1,3,5,6], 7
输出: 4

示例 4:
输入: [1,3,5,6], 0
输出: 0

# 我的解法
## 解题思路
找到给定数在排序好的数组中的位置，如果不在就返回顺序插入的位置
## 实现代码
### python
```python
class Solution:
    def searchInsert(self, nums: List[int], target: int) -> int:
        for i in range(0, len(nums)):
            if target <= nums[i]:
                return i
        return len(nums)

```

执行用时：40 ms, 在所有 Python3 提交中击败了75.05%的用户
内存消耗：14.3 MB, 在所有 Python3 提交中击败了63.75%的用户

### C++
```C++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        for (int i = 0; i < nums.size(); i++){
            if (target <= nums[i])
                return i;
        }
        return nums.size();
    }
};
```
执行用时：4 ms, 在所有 C++ 提交中击败了96.06%的用户
内存消耗：6.6 MB, 在所有 C++ 提交中击败了58.40%的用户

## 二分查找
还是应该用二分查找的方法才能达到log(n)的复杂度。只需要一直保证下界是小于target，然后返回下界即可
```C++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int lower = 0, upper = nums.size() - 1;
        int mid = 0;
        while (lower <= upper){
            mid = (upper - lower) / 2 + lower;
            if (nums[mid] < target)
                lower = mid + 1;
            else
                upper = mid - 1;
        }
        return lower;
    }
};

```
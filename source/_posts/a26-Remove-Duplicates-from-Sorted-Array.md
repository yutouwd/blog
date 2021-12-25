---
title: 26.Remove Duplicates from Sorted Array
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 3324950855
date: 2019-07-11 10:51:50
---
# 题目描述
Given a sorted array nums, remove the duplicates in-place such that each element appear only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

Example 1:
Given nums = [1,1,2],
Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the returned length.

Example 2:
Given nums = [0,0,1,1,1,2,2,3,3,4],
Your function should return length = 5, with the first five elements of nums being modified to 0, 1, 2, 3, and 4 respectively.
It doesn't matter what values are set beyond the returned length.


# 我的解法
## 解题思路
要将一个排列好的数组去掉重复的元素，然后返回长度。感觉挺简单的，可以用一个iterator和当前值对比，如果一样就erase掉，不一样就更新当前值，最后返回数组size。
## 实现代码
```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.size() == 0) return 0;
        int tmp = nums[0];
        vector<int>::iterator iter = nums.begin()+1;
        while(iter != nums.end()){
            if (*iter == tmp){
                iter = nums.erase(iter);
            }
            else{
                tmp = *iter;
                iter++;
            }
        }
        return nums.size();
    }
};
```

Runtime: 152 ms, faster than 19.92% of C++ online submissions for Remove Duplicates from Sorted Array.
Memory Usage: 9.9 MB, less than 63.90% of C++ online submissions for Remove Duplicates from Sorted Array.
# 代码改进
发现速度比较慢，看了下评论发现题目中没有要求要删掉重复的元素，erase的过程导致时间比较长。所以可以用将不重复的元素放到数组的前面。
It doesn't matter what values are set beyond the returned length.
## 实现代码
```C++
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        if (nums.size() == 0) return 0;
        if (nums.size() == 1) return 1;
        int tmp = nums[0];
        int j = 1; //用于记录有多少不重复的数字
        for (int i = 1; i < nums.size();i++){
            if (nums[i] == tmp){
                continue;
            }
            else{
                tmp = nums[i];
                nums[j] = nums[i];
                j++;
            }
        }
        return j;
    }
};
```
Runtime: 20 ms, faster than 94.92% of C++ online submissions for Remove Duplicates from Sorted Array.
Memory Usage: 10 MB, less than 21.43% of C++ online submissions for Remove Duplicates from Sorted Array.


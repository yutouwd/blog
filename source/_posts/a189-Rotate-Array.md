---
title: 189.Rotate Array
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 4112301143
date: 2019-07-17 15:26:11
---
# 题目描述
Given an array, rotate the array to the right by k steps, where k is non-negative.

Example 1:
Input: [1,2,3,4,5,6,7] and k = 3
Output: [5,6,7,1,2,3,4]
Explanation:
rotate 1 steps to the right: [7,1,2,3,4,5,6]
rotate 2 steps to the right: [6,7,1,2,3,4,5]
rotate 3 steps to the right: [5,6,7,1,2,3,4]

Example 2:
Input: [-1,-100,3,99] and k = 2
Output: [3,99,-1,-100]
Explanation: 
rotate 1 steps to the right: [99,-1,-100,3]
rotate 2 steps to the right: [3,99,-1,-100]
Note:

* Try to come up as many solutions as you can, there are at least 3 different ways to solve this problem.
* Could you do it in-place with O(1) extra space?

# 我的解法
## 解题思路
题目要求讲一个数组向右移动几位，最先想到的办法就是另外声明一个数组，然后将位移后的数组存到新数组里，最后再将新数组复制到旧数组里。
## 实现代码
```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        int n = nums.size();
        vector<int> tmp(n);
        k = k % n;
        for (int i = 0; i < nums.size(); i++){
            int j = i + k;
            if (j >= n)
                j = j - n;
            tmp[j] = nums[i];
        }
        nums = tmp;
    }
};
```

Runtime: 16 ms, faster than 88.16% of C++ online submissions for Rotate Array.
Memory Usage: 9.6 MB, less than 50.79% of C++ online submissions for Rotate Array.
# 优化方法1
提示说能不能用O(1)的方法，想了一下没有想到条件要怎么设置。看了下讨论区，有一种环状替换的方法
## 实现代码
```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if (k > nums.size()) k = k % nums.size();
        int count = 0;  //count 用来记录一共移动了多少次
        for (int i = 0; count < nums.size(); i++){
            int curr = i; //curr用于记录起始位置
            int prev = nums[i]; //prev用于记录替换前的数值
            do{
                int next = (curr + k) % nums.size(); //next为将要替换的位置
                int tmp = nums[next];
                nums[next] = prev;
                prev = tmp;
                curr = next;  //更新当前位置
                count++;
            }while (i != curr); //如果没有回到起点的话就一直继续下去
        }
    }
};
```

# 优化方法2
还看到一个用reverse的方法，只需要4行代码...
## 实现代码
```C++
class Solution {
public:
    void rotate(vector<int>& nums, int k) {
        if (k > nums.size()) k = k % nums.size();
        reverse(nums.begin(),nums.end());
        reverse(nums.begin(),nums.begin() + k);
        reverse(nums.begin() + k,nums.end());
    }
};
```
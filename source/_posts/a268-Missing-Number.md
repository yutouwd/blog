---
title: 268.Missing Number
tags:
  - leetcode
  - math
  - hashmap
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2942226103
date: 2020-02-17 17:38:07
---
# 题目描述
Given an array containing n distinct numbers taken from 0, 1, 2, ..., n, find the one that is missing from the array.

Example 1:
Input: [3,0,1]
Output: 2

Example 2:
Input: [9,6,4,2,3,5,7,0,1]
Output: 8

Note:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

# 我的解法
## 解题思路
最先想到的方法就是使用一个bool数组，大小要比输入的数组大一，全部初始化为true。然后遍历输入的数组，已输入数组中的数字为索引，将bool数组中的对应位置改为false。最后再遍历一遍bool数组，遇到了true就返回索引值。

## 实现代码
```C++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        vector<bool> miss(nums.size() + 1, true);
        for (int i = 0; i < nums.size(); i++)
            miss[nums[i]] = false;
        for (int i = 0; i< nums.size() + 1; i++){
            if (miss[i])
                return i;
        }
        return 0;
    }
};
```
Runtime: 24 ms, faster than 81.97% of C++ online submissions for Missing Number.
Memory Usage: 10 MB, less than 45.10% of C++ online submissions for Missing Number.
# 高票解法
## 实现代码
看了下题解，可以使用哈希表：
```C++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        set<int> s(nums.begin(), nums.end());
        for (int i = 0; i < nums.size() + 1; i++){
            if (s.find(i) == s.end())
                return i;
        }
        return 0;
    }
};
```
但是不知道为什么速度那么慢

Runtime: 68 ms, faster than 6.52% of C++ online submissions for Missing Number.
Memory Usage: 17.6 MB, less than 5.88% of C++ online submissions for Missing Number.

还可以使用数学方法，把整个数组加起来和0~n的等差数列求差，差值就是缺失值。为了防止数值溢出可以用边加边减的方法：

```C++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int sum = 0, i = 0;
        for (; i < nums.size(); i++)
            sum += nums[i] - i;
        sum -= i;
        return abs(sum);
    }
};
```

Runtime: 24 ms, faster than 81.97% of C++ online submissions for Missing Number.
Memory Usage: 9.9 MB, less than 72.55% of C++ online submissions for Missing Number.

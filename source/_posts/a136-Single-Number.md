---
title: 136.Single Number
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 1550415194
date: 2019-07-21 21:31:25
---
# 题目描述
Given a non-empty array of integers, every element appears twice except for one. Find that single one.

Note:

Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

Example 1:
Input: [2,2,1]
Output: 1

Example 2:
Input: [4,1,2,1,2]
Output: 4
# 我的解法
## 解题思路
可以先将数组进行排序，再和两边的数字进行比较，如果都不一样就是要找的的数字。
## 实现代码
```C++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        if (nums.size() == 1)
            return nums[0];
        sort(nums.begin(),nums.end());
        if (nums[0] != nums[1])
            return nums[0];
        for (int i = 1; i < nums.size()-1; i++){
            if (nums[i] != nums[i+1] && nums[i] != nums[i-1])
                return nums[i];
        }
        return nums[nums.size()-1];
    }
};
```

Runtime: 20 ms, faster than 37.49% of C++ online submissions for Single Number.
Memory Usage: 9.7 MB, less than 53.92% of C++ online submissions for Single Number.

# 高票解法
速度还是稍微慢了点的，看看高票的解法吧～
看到有好巧妙的方法，比如用按位异或的方法。因为相同的数字异或是等于0的，并且一个数和0异或的结果还是这个数，异或也符合交换律。所以将数组里的数全部按位异或，最后就可以得到只出现一次的数字了。
## 实现代码
```C++
class Solution {
public:
    int singleNumber(vector<int>& nums) {
        int num = 0;
        for (int i = 0; i < nums.size(); i++)
            num ^= nums[i];
        return num;
    }
};
```

Runtime: 16 ms, faster than 73.30% of C++ online submissions for Single Number.
Memory Usage: 9.6 MB, less than 82.15% of C++ online submissions for Single Number.



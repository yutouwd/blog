---
title: 66.Plus One
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 353015550
date: 2019-07-22 21:19:25
---
# 题目描述
Given a non-empty array of digits representing a non-negative integer, plus one to the integer.

The digits are stored such that the most significant digit is at the head of the list, and each element in the array contain a single digit.

You may assume the integer does not contain any leading zero, except the number 0 itself.

Example 1:

Input: [1,2,3]
Output: [1,2,4]
Explanation: The array represents the integer 123.
Example 2:

Input: [4,3,2,1]
Output: [4,3,2,2]
Explanation: The array represents the integer 4321.
# 我的解法
## 解题思路
可以先设计一个函数，将输入值加一并且返回是否有进位，有进位就返回true，没有返回false。然后在主程序里写个for循环，如果一直有进位就循环继续，没有进位的话就跳出循环。最后还要判断下数组的第一位是不是零，如果是零就在数组的开头插入一个1。
## 实现代码
```C++
class Solution {
public:
    bool addOneCarry(int& digit){
        if (digit == 9){
            digit = 0;
            return true;
        }
        else{
            digit++;
            return false;
        }
    }
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size();
        for (int i = n-1; i >= 0; i--){
            if (addOneCarry(digits[i]))
                continue;
            else
                break;
        }
        if (digits[0] == 0)
            digits.insert(digits.begin(),1);
        return digits;
    }
};
```
Runtime: 4 ms, faster than 73.90% of C++ online submissions for Plus One.
Memory Usage: 8.6 MB, less than 49.35% of C++ online submissions for Plus One.
# 高票解法
看了看评论，发现其实可以简化一下程序的。直接判断当前位是不是9就可以了。
## 实现代码
```C++
class Solution {
public:
    vector<int> plusOne(vector<int>& digits) {
        int n = digits.size();
        for (int i = n-1; i >= 0; i--){
            if (digits[i] == 9)
                digits[i] = 0;
            else{
                digits[i]++;
                break;
            }
        }
        if (digits[0] == 0)
            digits.insert(digits.begin(),1);
        return digits;
    }
};
```

Runtime: 4 ms, faster than 73.90% of C++ online submissions for Plus One.
Memory Usage: 8.5 MB, less than 69.58% of C++ online submissions for Plus One.


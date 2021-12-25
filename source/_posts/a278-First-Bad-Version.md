---
title: 278.First Bad Version
tags:
  - leetcode
  - math
  - 二分查找
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 539789119
date: 2019-12-28 23:30:18
---
# 题目描述
You are a product manager and currently leading a team to develop a new product. Unfortunately, the latest version of your product fails the quality check. Since each version is developed based on the previous version, all the versions after a bad version are also bad.

Suppose you have n versions [1, 2, ..., n] and you want to find out the first bad one, which causes all the following ones to be bad.

You are given an API bool isBadVersion(version) which will return whether version is bad. Implement a function to find the first bad version. You should minimize the number of calls to the API.

Example:

Given n = 5, and version = 4 is the first bad version.

call isBadVersion(3) -> false
call isBadVersion(5) -> true
call isBadVersion(4) -> true

Then 4 is the first bad version. 
# 我的解法
## 解题思路
可以用二分搜索来做。
## 实现代码
```C++
// Forward declaration of isBadVersion API.
bool isBadVersion(int version);
class Solution {
public:
    int firstBadVersion(int n) {
        if (n == 1) return n;
        if (n == 2) return isBadVersion(1) ? 1 : 2;
        long long upper = n, lower = 1;
        bool upper_bad = isBadVersion(upper);
        bool lower_bad = isBadVersion(lower);
        bool middle_bad;
        long long middle = 1;
        do {
            middle = (upper + lower) / 2;
            middle_bad = isBadVersion(middle);
            if (middle_bad == upper_bad)
                upper = middle;
            else 
                lower = middle;
        } while((upper - lower != 1));
        if (isBadVersion(lower))
            return lower;
        return upper;
    }
};

```
Runtime: 4 ms, faster than 52.02% of C++ online submissions for First Bad Version.
Memory Usage: 8.2 MB, less than 48.48% of C++ online submissions for First Bad Version.

# 高票解法
代码还有可以优化的地方
比如可以通过下面这种方式来避免int型的溢出，并且可以不用使用long型。
```C++
int middle = lower + (upper - lower) / 2;
```
并且使用更加精简的二分查找，需要注意的是判断带不带等于，和返回的值。

这里我们需要找到一个值，他会返回true同时他减一会返回false。使用二分查找，如果中间值返回了true，那么证明我们要找的值在左边，并且这个中间值有可能就是我们要找的数，所以把右界设置为中间值；如果中间值返回了false，那么证明我们要找的数还在右边，并且不可能是中间值，所以把左界调整为中间值加一。
## 实现代码
```C++
// Forward declaration of isBadVersion API.
bool isBadVersion(int version);

class Solution {
public:
    int firstBadVersion(int n) {
        int upper = n, lower = 1;
        while (lower < upper){
            int middle = lower + (upper - lower) / 2;
            if (isBadVersion(middle))
                upper = middle;
            else
                lower = middle + 1;
        }
        return lower;
    }
};
```

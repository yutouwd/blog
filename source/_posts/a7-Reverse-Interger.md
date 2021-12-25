---
title: 7.Reverse Interger
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 1020379111
date: 2019-04-08 20:29:30
mathjax: true
---
# 题目描述
Given a 32-bit signed integer, reverse digits of an integer. 

Example 1: 
Input: 123 
Output: 321 

Example 2: 
Input: -123 
Output: -321 

Example 3: 
Input: 120 
Output: 21 

Note: 
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows. 
# 我的解法
## 解题思路
给一个32位的整数，然后将这个数反转过来。如果反转过来的数溢出了，就返回0。
## 实现代码
```C++
class Solution {
public:
    int reverse(int x) {
        int y = 0, z = 0;
        while(x){
            y = z * 10 + x % 10;
            if (y / 10 != z)
                return 0;
            z = y;
            x /= 10;
        }
        return z;
    }
};
```
这个是之前不知道多久做的了，之前是可以Accepted的，但是现在会报runtime error: singled integer overflow: 964632435 * 10 cannot be represented in type 'int'. 现在溢出都会有检查了吗。。。

# 高票解法
来看看官方的solution吧。
## 思路分析
它的思路其实很简单：
> 就是重复的将x的最后一位pop出来，然后再push到rev中，最后rev就储存了反转后的结果了。但是只是这么做是很危险的，因为会产生溢出。但幸运的是有简单的办法在溢出前进行检查，假设x为正数。
* 如果\\(temp=rev*10+pop\\)导致溢出，所以就有\\(rev>=\frac{INTMAX}{10}\\)
* 如果\\(rev>\frac{INTMAX}{10}\\)，那么\\(temp=rev*10+pop\\)一定会溢出
* 如果\\(rev=\frac{INTMAX}{10}\\)，那么\\(temp=rev*10+pop\\)会溢出当\\(pop>7\\)

当x为负数的时候，逻辑是一样的，不过就是要将第三点改为\\(pop<-8\\)，因为int型的范围是[-2147483648,2147483647]
## 实现代码
```C++
public:
    int reverse(int x) {
        int rev = 0;
        while (x != 0) {
            int pop = x % 10;
            x /= 10;
            if (rev > INT_MAX/10 || (rev == INT_MAX / 10 && pop > 7)) return 0;
            if (rev < INT_MIN/10 || (rev == INT_MIN / 10 && pop < -8)) return 0;
            rev = rev * 10 + pop;
        }
        return rev;
    }
};
```
代码时间复杂度为O(logx)
# 知识总结
学习了检查int型溢出的方法。
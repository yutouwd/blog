---
title: 50.Pow(x,n)
tags:
  - leetcode
  - math
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 2356977837
date: 2019-10-11 13:25:25
---
# 题目描述
Implement pow(x, n), which calculates x raised to the power n (xn).

Example 1:
Input: 2.00000, 10
Output: 1024.00000

Example 2:
Input: 2.10000, 3
Output: 9.26100

Example 3:
Input: 2.00000, -2
Output: 0.25000
Explanation: 2-2 = 1/22 = 1/4 = 0.25

Note:
-100.0 < x < 100.0
n is a 32-bit signed integer, within the range [−2^31, 2^31 − 1]
# 我的解法
## 解题思路
计算一个数的幂，最先想到的方法就是用循环的方法，但是要考虑好当n=0或者n小于0的情况。
## 实现代码
```C++
class Solution {
public:
    double myPow(double x, int n) {
        if (x == 0)
            return 0;
        if (n == 0)
            return 1.0;
        double ans = x;
        if (n < 0 && x != 0){
            x = 1/x;
            ans = x;
            n = -n;
        }
        for (int i = 1; i < n; i++)
            ans *= x;
        return ans;
    }
};
```
当输入为：
0.00001
2147483647
会超出时间限制
# 高票解法
于是去看了看官方解法
## 快速幂算法-递归
```C++
class Solution {
public:
    double fastPow(double x, long long n) {
        if (n == 0) {
            return 1.0;
        }
        double half = fastPow(x, n / 2);
        if (n % 2 == 0) {
            return half * half;
        } else {
            return half * half * x;
        }
    }
    double myPow(double x, int n) {
        long long N = n;
        if (N < 0) {
            x = 1 / x;
            N = -N;
        }
        return fastPow(x, N);
    }
};
```

思路就是，当我们知道了x^n时，我们就可以快速的求出x^2n，而不需要在将x乘n次
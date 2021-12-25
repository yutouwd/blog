---
title: 70.Climbing Stairs
tags:
  - leetcode
  - math
  - 分治法
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 1665362949
date: 2019-07-28 17:52:21
---
# 题目描述
You are climbing a stair case. It takes n steps to reach to the top.

Each time you can either climb 1 or 2 steps. In how many distinct ways can you climb to the top?

Note: Given n will be a positive integer.

Example 1:
Input: 2
Output: 2
Explanation: There are two ways to climb to the top.
1. 1 step + 1 step
2. 2 steps

Example 2:
Input: 3
Output: 3
Explanation: There are three ways to climb to the top.
1. 1 step + 1 step + 1 step
2. 1 step + 2 steps
3. 2 steps + 1 step


# 我的解法
## 解题思路
[之前看过一篇博客讲分治法就见到了这道题目][1]。分治法就是Divide and Conquer，流程有三步：
> * 分解（Divide）将大规模的问题分解成若干个规模更小但形式相同的子问题
  * 解决（Conquer）如果当前问题的规模足够小，并可以直接解决的话，那么直接解决并返回解。否则，继续进行分解并递归求解分解后的子问题。
  * 合并（Merge）将各个子问题合并，最终形成原问题的解。


通常可以通过递归的方式来实现分治法，就这道问题而言，如果当前在走第n步，那么可以把问题分解为走n-1步（当前走1个台阶）和n-2步（当前走两个台阶），即f(n)=f(n-1)+f(n-2)，当n等于1或2的时候，就分别只有1或2种走法了。
## 实现代码
```C++
class Solution {
public:
    int climbStairs(int n) {
        if (n > 2)
            return climbStairs(n - 1) + climbStairs(n - 2);
        if (n <= 2 && n > 0)
            return n;
        return 0;
    }
};
```

但是如果用递归的话，会在n等于44的时候超出时间限制
# 高票解法
也可以用for循环来完成这个问题
## 实现代码
```C++
class Solution {
public:
    int climbStairs(int n) {
        if (n <= 2)
            return n;
        int pre = 1;
        int now = 2;
        for (int i = 3; i <= n; i++){
            int tmp = now;
            now += pre;
            pre = tmp;
        }
        return now;
    }
};
```
## 代码分析
其实思路也很简单，就是用pre记录n-1的方法数，now来记录n的方法数，然后每个for循环中都更新now和pre。当进行到n+1的时候，now就等于之前的now加上pre。



[1]:http://blog.ihuxu.com/divide-and-conquer-backtracking-and-dynamic-programming-from-a-frog-jumping-out/
---
title: 9.Palindrome Number
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 837075
date: 2019-04-11 11:42:41
---
# 题目描述
Determine whether an integer is a palindrome. An integer is a palindrome when it reads the same backward as forward.

Example 1:
Input: 121
Output: true

Example 2:
Input: -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

Example 3:
Input: 10
Output: false
Explanation: Reads 01 from right to left. Therefore it is not a palindrome.

Follow up:
Coud you solve it without converting the integer to a string?
# 我的解法
## 解题思路
题目要求是判断一个数是不是palindrome。一个数如果是palindrome，那么它从左往右读和从右往左读都是一样的。并且负数不是palindrome。并且最好在不将整数转换为string的情况下完成。

其实可以用[第七题][1]第思路，只要一个数反转过来和它相等，那么它就是palindrome。
## 实现代码
```C++
class Solution {
public:
    bool isPalindrome(int x) {
        if (x < 0){
            return false;
        }
        if (x < 10 && x >= 0){
            return true;
        }
        int rev = 0, x_val = x;
        while(x != 0) {
            int pop = x % 10;
            x /= 10;
            if (rev > INT_MAX/10 || (rev == INT_MAX / 10 && pop > 7))
                return false;
            rev = rev * 10 + pop;
        }
        if (rev == x_val){
            return true;
        }
        else
            return false;
    }
};
```
✔ Accepted
  ✔ 11509/11509 cases passed (32 ms)
  ✔ Your runtime beats 99.62 % of cpp submissions
  ✔ Your memory usage beats 99.33 % of cpp submissions (8.2 MB)


[1]:https://yutouwd.github.io/posts/1020379111


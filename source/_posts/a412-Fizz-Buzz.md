---
title: 412.Fizz Buzz
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 807358486
date: 2019-09-10 14:42:09
---
# 题目描述
Write a program that outputs the string representation of numbers from 1 to n.

But for multiples of three it should output “Fizz” instead of the number and for the multiples of five output “Buzz”. For numbers which are multiples of both three and five output “FizzBuzz”.

Example:

n = 15,

Return:
[
    "1",
    "2",
    "Fizz",
    "4",
    "Buzz",
    "Fizz",
    "7",
    "8",
    "Fizz",
    "Buzz",
    "11",
    "Fizz",
    "13",
    "14",
    "FizzBuzz"
]

# 我的解法
## 解题思路
这道题比较简单
## 实现代码
```C++
class Solution {
public:
    vector<string> fizzBuzz(int n) {
        vector<string> output;
        for (int i = 1; i <= n; i++){
            int mod3 = i % 3;
            int mod5 = i % 5;
            if (mod5 == 0 && mod3 == 0)
                output.push_back("FizzBuzz");
            else if (mod3 == 0 && mod5 != 0)
                output.push_back("Fizz");
            else if (mod5 == 0 && mod3 != 0)
                output.push_back("Buzz");
            else
                output.push_back(to_string(i));
        }
        return output;
    }
};
```


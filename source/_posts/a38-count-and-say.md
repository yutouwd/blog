---
title: 38.Count and Say
tags:
  - leetcode
  - string
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2107205244
date: 2019-04-26 16:29:00
---
# 题目描述
The count-and-say sequence is the sequence of integers with the first five terms as following:

1. 1
2. 11
3. 21
4. 1211
5. 111221

1 is read off as "one 1" or 11.
11 is read off as "two 1s" or 21.
21 is read off as "one 2, then one 1" or 1211.

Given an integer n where 1 ≤ n ≤ 30, generate the nth term of the count-and-say sequence.

Note: Each term of the sequence of integers will be represented as a string.

Example 1:

Input: 1
Output: "1"
Example 2:

Input: 4
Output: "1211"

# 我的解法
## 解题思路
看完这个题目真的一头雾水，完全没有理解题目要干什么，看了下discuss里面有一个不错的题目解读：
> 初始值第一行是 1。
第二行读第一行，1 个 1，去掉个字，所以第二行就是 11。
第三行读第二行，2 个 1，去掉个字，所以第三行就是 21。
第四行读第三行，1 个 2，1 个 1，去掉所有个字，所以第四行就是 1211。
第五行读第四行，1 个 1，1 个 2，2 个 1，去掉所有个字，所以第五航就是 111221。
第六行读第五行，3 个 1，2 个 2，1 个 1，去掉所以个字，所以第六行就是 312211。
然后题目要求输入 1 - 30 的任意行数，输出该行是啥。

题目还说输入是在1～30之内的一个整数，所以可以从1开始数，一直数到输入的数字。

## 实现代码
```C++
class Solution {
public:
    string countAndSay(int n) {
        string str = "1";
        while(--n){
            string tmp;
            int count = 1;
            for(auto iter = str.begin();iter != str.end();iter++){
                if (*iter == *(iter + 1)){
                    count++;
                }
                else{
                    tmp += to_string(count);
                    tmp += (*iter);
                    count = 1;
                }
            }
            str = tmp;
        }
        return str;
    }
};
```

Runtime: 4 ms, faster than 100.00% of C++ online submissions for Count and Say.
Memory Usage: 8.9 MB, less than 57.06% of C++ online submissions for Count and Say.

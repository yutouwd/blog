---
title: 195.Tenth Line
tags:
  - leetcode
categories:
  - leetcode
copyright: true
comments: true
notshow: true
abbrlink: 633169037
date: 2020-02-18 12:12:55
---
# 题目描述
Given a text file file.txt, print just the 10th line of the file.

Example:

Assume that file.txt has the following content:

Line 1
Line 2
Line 3
Line 4
Line 5
Line 6
Line 7
Line 8
Line 9
Line 10

Your script should output the tenth line, which is:
Line 10
# 我的解法
## 解题思路
```Bash
awk 'NR==10' file.txt
```

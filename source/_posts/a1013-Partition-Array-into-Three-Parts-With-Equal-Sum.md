---
title: 1013.Partition Array into Three Parts with Equal Sum
tags:
  - leetcode
  - math
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 1190621326
date: 2020-03-23 19:13:25
---
# 题目描述
Given an array A of integers, return true if and only if we can partition the array into three non-empty parts with equal sums.

Formally, we can partition the array if we can find indexes i+1 < j with (A[0] + A[1] + ... + A[i] == A[i+1] + A[i+2] + ... + A[j-1] == A[j] + A[j-1] + ... + A[A.length - 1])

Example 1:
Input: A = [0,2,1,-6,6,-7,9,1,2,0,1]
Output: true
Explanation: 0 + 2 + 1 = -6 + 6 - 7 + 9 + 1 = 2 + 0 + 1

Example 2:
Input: A = [0,2,1,-6,6,7,9,-1,2,0,1]
Output: false

Example 3:
Input: A = [3,3,6,5,-2,2,5,1,-9,4]
Output: true
Explanation: 3 + 3 = 6 = 5 - 2 + 2 + 5 + 1 - 9 + 4
 
Constraints:
3 <= A.length <= 50000
-10^4 <= A[i] <= 10^4
# 我的解法
## 解题思路
判断一个数组能不能被分为3个相等的部分，首先先计算数组总和，如果不能被3整除返回false。然后遍历数组，求每个元素相加有多少次等于sum/3，如果次数等于2次并且没有遍历到最后一个元素就返回true。
## 实现代码
```C++
class Solution {
public:
    bool canThreePartsEqualSum(vector<int>& A) {
        int sum = accumulate(A.begin(), A.end(), 0);
        if (A.size() < 3 || sum % 3 != 0)
            return false;
        int target = sum / 3, times = 0, tmp = 0;
        for (int i = 0; i < A.size(); i++){
            tmp += A[i];
            if (tmp == target){
                times++;
                tmp = 0;
            }
            if (times == 2 && i != A.size() - 1)
                return true;
        }
        return false;
    }
};
```

Runtime: 68 ms, faster than 55.54% of C++ online submissions for Partition Array Into Three Parts With Equal Sum.
Memory Usage: 10.7 MB, less than 100.00% of C++ online submissions for Partition Array Into Three Parts With Equal Sum.

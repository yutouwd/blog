---
title: 349.Intersection of Two Arrays
tags:
  - leetcode
  - hashmap
  - vector
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 1952106908
date: 2019-12-10 23:55:29
---
# 题目描述
Given two arrays, write a function to compute their intersection.

Example 1:
Input: nums1 = [1,2,2,1], nums2 = [2,2]
Output: [2]

Example 2:
Input: nums1 = [4,9,5], nums2 = [9,4,9,8,4]
Output: [9,4]

Note:
Each element in the result must be unique.
The result can be in any order.

# 我的解法
## 解题思路
统计两个数组重复出现的数字，返回的数组每个数字都是不重复。使用两个unordered_map来记录两个数组每个数字出现的次数，然后如果如果存在相同的就加到答案数组中。
## 实现代码
```C++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_map<int, int> count1;
        unordered_map<int, int> count2;
        for (int i : nums1)
            count1[i]++;
        for (int i : nums2)
            count2[i]++;
        vector<int> ans;
        for (auto i : count1){
            if (count2.find(i.first) != count2.end())
                ans.push_back(i.first);
        }
        return ans;
    }
};
```
Runtime: 4 ms, faster than 99.17% of C++ online submissions for Intersection of Two Arrays.
Memory Usage: 9.8 MB, less than 10.00% of C++ online submissions for Intersection of Two Arrays.
# 高票解法
看了下高票的解答，发现其实可以用set来实现。用set来记录第一个数组中出现的数字，然后在遍历第二个数组，如果有出现的话就加到答案数组中去，并把set中的erase掉。

## 实现代码
```C++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> s(nums1.begin(), nums1.end());
        vector<int> ans;
        for (auto i : nums2){
            if (s.count(i)){
                ans.push_back(i);
                s.erase(i);
            }
        }
        return ans;
    }
};
```
Runtime: 4 ms, faster than 99.17% of C++ online submissions for Intersection of Two Arrays.
Memory Usage: 9.4 MB, less than 50.00% of C++ online submissions for Intersection of Two Arrays.
# 知识总结
学习了set的用法，如果把一个数组统计到set中可以直接用将begin和end输入到set中就可以了。
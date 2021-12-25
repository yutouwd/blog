---
title: 215.Kth Largest Element in an Array
tags:
  - leetcode
  - vector
  - math
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 2993655736
date: 2019-10-28 13:51:05
---
# 题目描述
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.

Example 1:
Input: [3,2,1,5,6,4] and k = 2
Output: 5

Example 2:
Input: [3,2,3,1,2,4,5,5,6] and k = 4
Output: 4

Note:
You may assume k is always valid, 1 ≤ k ≤ array's length.
# 我的解法
## 解题思路
可以想把数组排序，然后在返回第k大的数字就可以了
## 实现代码
```C++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end());
        return nums[nums.size() - k];
    }
};
```
Runtime: 12 ms, faster than 77.71% of C++ online submissions for Kth Largest Element in an Array.
Memory Usage: 9.2 MB, less than 89.39% of C++ online submissions for Kth Largest Element in an Array.
# 高票解法
C++中排序的时间复杂度为O(NlogN)，如果使用优先队列，对于插入一个大小为k的优先队列插入N次，时间复杂度为O(Nlogk)也可以使用C++中的priority_queue优先队列，默认是大顶堆。
## 实现代码
```C++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int> pq(nums.begin(), nums.end());
        for (int i = 0; i < k - 1; i++){
            pq.pop();
        }
        return pq.top();
    }
};
```
Runtime: 8 ms, faster than 97.45% of C++ online submissions for Kth Largest Element in an Array.
Memory Usage: 9.5 MB, less than 40.91% of C++ online submissions for Kth Largest Element in an Array.
## 代码分析
还可以进一步优化一下，使堆的大小最多保持在k
```C++
class Solution {
public:
    int findKthLargest(vector<int>& nums, int k) {
        priority_queue<int, vector<int>, greater<int>> pq;
        for(int num : nums){
            if (pq.size() == k){
                if (num > pq.top()){
                    pq.pop();
                    pq.push(num);
                }
            }
            else
                pq.push(num);
        }
        return pq.top();
    }
};
```
Runtime: 8 ms, faster than 97.45% of C++ online submissions for Kth Largest Element in an Array.
Memory Usage: 9.5 MB, less than 33.33% of C++ online submissions for Kth Largest Element in an Array.
# 知识总结
学习了C++中priority_queue的使用
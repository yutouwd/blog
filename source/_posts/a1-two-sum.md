---
title: 1.Two Sum
tags:
  - leetcode
  - vector
  - hashmap
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2304652807
date: 2019-04-05 08:43:29
---
# 题目描述
Given an array of integers, return indices of the two numbers such that they add up to a specific target. 

You may assume that each input would have exactly one solution, and you may not use the same element twice. 

Example: 


Given nums = [2, 7, 11, 15], target = 9, 

Because nums[0] + nums[1] = 2 + 7 = 9, 
return [0, 1]. 

# 我的解法
## 解题思路
题目的意思是给到一个整形的数组和一个目标，要在这个数组里面找到两个数相加等于这个目标的两个数，并返回这两个数的索引数组。并且可以假定每个输入必有且只有一个解，不能用一个数两次。

简单的想法就是用两个for循环，遍历数组里两个数相加的组合，如果相加等于目标，就返回这两个索引值。

## 实现代码
```C++
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int> index;
        for (int i = 0; i < nums.size() - 1;i++){
            for (int j = i + 1; j < nums.size(); j++){
                if (nums[i] + nums[j] == target){
                    index.push_back(i);
                    index.push_back(j);
                    return index;
                }
            }
        }
        return index;
    }
};
```
结果如下：
✔ Accepted
  ✔ 29/29 cases passed (144 ms)
  ✔ Your runtime beats 32.13 % of cpp submissions
  ✔ Your memory usage beats 99.9 % of cpp submissions (9.2 MB)
速度有点点的慢

# 高票解法
看了下高票以及速度较快的解法，基本都是用了hash表。之前做题的时候也经常可以见到，但是一直也都没有太理解它的用法
## 实现代码
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> indices;
        for (int i = 0; i < nums.size(); i++) {
            if (indices.find(target - nums[i]) != indices.end()) {
                return {indices[target - nums[i]], i};
            }
            indices[nums[i]] = i;
        }
        return {};
    }
};
```


# 知识总结
先好好了解一下哈希表和C++中的map和inorder_map的用法。


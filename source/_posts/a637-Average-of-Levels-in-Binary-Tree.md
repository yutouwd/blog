---
title: 637.Average of Levels in Binary Tree
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 1794294162
date: 2020-09-12 10:03:14
---
# 题目描述
Given a non-empty binary tree, return the average value of the nodes on each level in the form of an array.
Example 1:
Input:
    3
   / \
  9  20
    /  \
   15   7
Output: [3, 14.5, 11]
Explanation:
The average value of nodes on level 0 is 3,  on level 1 is 14.5, and on level 2 is 11. Hence return [3, 14.5, 11].
Note:
The range of node's value is in the range of 32-bit signed integer.


# 我的解法
## 解题思路
这道题目比较简单，就是求二叉树的每一层的均值，使用层次遍历即可。
## 实现代码
```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        vector<double> res;
        if (root == nullptr)
            return res;
        queue<TreeNode*> q;
        q.push(root);
        while(!q.empty()){
            double sum = 0;
            int n = q.size();
            for (int i = 0; i < n; i++){
                TreeNode* node = q.front();
                q.pop();
                sum += node -> val;
                if (node -> left != nullptr) q.push(node -> left);
                if (node -> right!= nullptr) q.push(node -> right);
            }
            res.push_back((double) sum / (double) n);
        }
        return res;
    }
};
```
执行用时：20 ms, 在所有 C++ 提交中击败了97.35%的用户
内存消耗：22.7 MB, 在所有 C++ 提交中击败了51.42%的用户
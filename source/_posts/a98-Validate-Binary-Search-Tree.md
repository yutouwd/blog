---
title: 98.Validate Binary Search Tree
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - Medium
copyright: true
comments: true
notshow: true
abbrlink: 521402559
date: 2019-11-29 23:02:45
---
# 题目描述
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

The left subtree of a node contains only nodes with keys less than the node's key.
The right subtree of a node contains only nodes with keys greater than the node's key.
Both the left and right subtrees must also be binary search trees.
 

Example 1:

    2
   / \
  1   3
Input: [2,1,3]
Output: true

Example 2:

    5
   / \
  1   4
     / \
    3   6
Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.

# 我的解法
## 解题思路
一开始似乎理解错了题目的意思
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
    bool isValidBST(TreeNode* root) {
        return isBST(root, LONG_MIN, LONG_MAX);
    }
    bool isBST(TreeNode* root, long lower, long upper){
        if (!root) return true;
        if (root -> val <= lower || root -> val >= upper) return false;
        bool left, right;
        left = isBST(root -> left, lower, root -> val);
        right = isBST(root -> right, root -> val, upper);
        return left && right;
    }
};
```
Runtime: 4 ms, faster than 99.97% of C++ online submissions for Validate Binary Search Tree.
Memory Usage: 20.6 MB, less than 86.46% of C++ online submissions for Validate Binary Search Tree.

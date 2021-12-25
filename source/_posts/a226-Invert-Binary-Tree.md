---
title: 226.Invert Binary Tree
tags:
  - leetcode
categories:
  - leetcode
copyright: true
comments: true
abbrlink: 3176726672
date: 2020-09-16 19:48:54
---
# 题目描述
Invert a binary tree.

Example:

Input:

     4
   /   \
  2     7
 / \   / \
1   3 6   9
Output:

     4
   /   \
  7     2
 / \   / \
9   6 3   1


# 我的解法
## 解题思路
翻转一个二叉树，最容易想到的方法就是递归了吧，先把当前节点的左右子树调换，然后在翻转当前节点的左子树和右子树。
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

    TreeNode* invertTree(TreeNode* root) {
        if (root == NULL) return NULL;
        TreeNode* tmp = root -> left;
        root -> left = root -> right;
        root -> right = tmp;
        root -> left = invertTree(root -> left);
        root ->right = invertTree(root ->right);
        return root;
    }
};
```

执行用时：0 ms, 在所有 C++ 提交中击败了100.00%的用户
内存消耗：9.2 MB, 在所有 C++ 提交中击败了23.25%的用户
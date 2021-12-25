---
title: 404.Sum of Left Leaves
tags:
  - leetcode
categories:
  - leetcode
copyright: true
comments: true
abbrlink: 3649739623
date: 2020-09-19 14:34:13
---
# 题目描述
Find the sum of all left leaves in a given binary tree.

Example:

    3
   / \
  9  20
    /  \
   15   7

There are two left leaves in the binary tree, with values 9 and 15 respectively. Return 24.

# 我的解法
## 解题思路
求二叉树的左子叶的和，可以通过递归的方法（深度优先）：
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
private:
    int res;
public:
    int sumOfLeftLeaves(TreeNode* root) {
        if (root == NULL) return 0;
        if (root -> left && root -> left -> left == NULL && root -> left -> right == NULL)
           res += root -> left -> val;
        if (root -> left) sumOfLeftLeaves(root -> left);
        if (root -> right) sumOfLeftLeaves(root -> right);
        return res;
    }
};
```
执行用时：8 ms, 在所有 C++ 提交中击败了51.83%的用户
内存消耗：13.1 MB, 在所有 C++ 提交中击败了71.76%的用户

再试试迭代的方法（广度优先）：
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
    int sumOfLeftLeaves(TreeNode* root) {
        if (root == NULL) return 0;
        queue<TreeNode*> q;
        q.push(root);
        int res = 0;
        while(!q.empty()){
            int n = q.size();
            for (int i = 0; i < n; i++){
                TreeNode* node = q.front();
                q.pop();
                if (node -> left && node -> left -> left == NULL && node -> left -> right == NULL){
                    res += node -> left -> val;
                }
                if (node -> left) q.push(node -> left);
                if (node -> right)q.push(node ->right);
            }
        }
        return res;
    }
};
```
执行用时：4 ms, 在所有 C++ 提交中击败了89.39%的用户
内存消耗：13.3 MB, 在所有 C++ 提交中击败了14.86%的用户
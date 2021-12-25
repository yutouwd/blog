---
title: 101.Symmetic Tree
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 1627979900
date: 2019-11-29 23:15:03
---
# 题目描述
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree [1,2,2,3,4,4,3] is symmetric:

    1
   / \
  2   2
 / \ / \
3  4 4  3
 

But the following [1,2,2,null,3,null,3] is not:

    1
   / \
  2   2
   \   \
   3    3
 
Note:
Bonus points if you could solve it both recursively and iteratively.

# 我的解法
## 解题思路
判断一个树是不是对称二叉树，可以使用两个队列，一个储存root左边的子树，一个储存root右边的子树。
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
    bool isSymmetric(TreeNode* root) {
        if (!root) return true;
        TreeNode *left, *right;
        queue<TreeNode*> q1, q2;
        q1.push(root -> left);
        q2.push(root -> right);
        
        while(!q1.empty() && !q2.empty()){
            left = q1.front();
            right = q2.front();
            q1.pop();
            q2.pop();
            if (left == NULL && right == NULL) continue;
            if (left == NULL && right != NULL) return false;
            if (left != NULL && right == NULL) return false;
            if (left -> val != right -> val) return false;
            q1.push(left -> left);
            q2.push(right -> right);
            q1.push(left -> right);
            q2.push(right -> left);
        }
        return true;
    }
};
```
Runtime: 4 ms, faster than 84.31% of C++ online submissions for Symmetric Tree.
Memory Usage: 15 MB, less than 37.29% of C++ online submissions for Symmetric Tree.

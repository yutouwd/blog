---
title: 107.Binary Tree Level Order Traversal II
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 4050777627
date: 2020-09-06 11:44:33
---
# 题目描述
Given a binary tree, return the bottom-up level order traversal of its nodes' values. (ie, from left to right, level by level from leaf to root).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its bottom-up level order traversal as:
[
  [15,7],
  [9,20],
  [3]
]
# 我的解法

## 解题思路
二叉树的层次遍历，而[#102]的不同在于返回数组是从下往上的。使用一个队列遍历从上往下，最后把数组反转一下。
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
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        vector<vector<int>> res;
        queue<TreeNode*> q;
        if (root == NULL)
            return res;
        q.push(root);
        while(!q.empty()){
            int n = q.size();
            vector<int> v;
            for (int i = 0; i < n; i++){
                TreeNode* node = q.front();
                q.pop();
                v.push_back(node -> val);
                if (node -> left != nullptr) q.push(node -> left);
                if (node -> right!= nullptr) q.push(node -> right);
            }
            res.push_back(v);
        }
        reverse(res.begin(), res.end());
        return res;
    }
};
```

执行用时：4 ms, 在所有 C++ 提交中击败了90.57%的用户
内存消耗：11.9 MB, 在所有 C++ 提交中击败了18.02%的用户

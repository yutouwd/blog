---
title: 102.Binary Tree Level Order Traversal
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 3533375508
date: 2019-11-15 22:08:04
---
# 题目描述
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its level order traversal as:
[
  [3],
  [9,20],
  [15,7]
]
# 我的解法
## 解题思路
层次遍历，可以用104题中的双向队列来实现
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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        if (root == NULL) return ans;
        deque<TreeNode*> q;
        q.push_back(root);
        while (!q.empty()){
            int n = q.size();
            vector<int> answer;
            for (int i = 0; i < n; i++){
                TreeNode* node = q.front();
                q.pop_front();
                answer.push_back(node -> val);
                if (node -> left) q.push_back(node -> left);
                if (node -> right) q.push_back(node -> right);
            }
            ans.push_back(answer);
        }
        return ans;
    }
};
```
Runtime: 4 ms, faster than 93.52% of C++ online submissions for Binary Tree Level Order Traversal.
Memory Usage: 13.7 MB, less than 98.59% of C++ online submissions for Binary Tree Level Order Traversal.

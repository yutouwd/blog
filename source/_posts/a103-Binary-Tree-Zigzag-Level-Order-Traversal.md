---
title: 103.Binary Tree Zigzag Level Order Traversal
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 2376334793
date: 2020-12-19 17:16:40
---
# 题目描述
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree [3,9,20,null,null,15,7],
    3
   / \
  9  20
    /  \
   15   7
return its zigzag level order traversal as:
[
  [3],
  [20,9],
  [15,7]
]


# 我的解法
## 解题思路
使用双向队列，奇数行的从左往右，偶数行的从右往左。
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
    vector<vector<int>> zigzagLevelOrder(TreeNode* root) {
        vector<vector<int>> res;
        if (root == nullptr) return res;
        deque<TreeNode*> q;
        q.push_back(root);
        bool front = true;
        while (!q.empty()){
            int n = q.size();
            vector<int> vec;
            if (front){
                for (int i = 0; i < n; i++){
                    TreeNode* tmp = q.front();
                    q.pop_front();
                    vec.push_back(tmp -> val);
                    if (tmp -> left) q.push_back(tmp -> left);
                    if (tmp -> right)q.push_back(tmp -> right);
                }
                front = false;

            }
            else{
                for (int i = 0; i < n; i++){
                    TreeNode* tmp  = q.back();
                    q.pop_back();
                    vec.push_back(tmp -> val);
                    if (tmp -> right)q.push_front(tmp -> right);
                    if (tmp -> left) q.push_front(tmp -> left);
                }
                front = true;
            }
            res.push_back(vec);
        }
        return res;
    }
};
```

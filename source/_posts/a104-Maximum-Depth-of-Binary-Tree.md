---
title: 104.Maximum Depth of Binary Tree
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 282883092
date: 2019-11-12 23:08:23
---
# 题目描述
Given a binary tree, find its maximum depth.

The maximum depth is the number of nodes along the longest path from the root node down to the farthest leaf node.

Note: A leaf is a node with no children.

Example:

Given binary tree [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
return its depth = 3.
# 我的解法
## 解题思路
可以用递归来实现深度优先的方法
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
    int maxDepth(TreeNode* root) {
        if (root == NULL)
            return 0;
        int l = maxDepth(root->left) + 1;
        int r = maxDepth(root->right) + 1;
        return l > r ? l : r;
    }
};
```

Runtime: 16 ms, faster than 21.06% of C++ online submissions for Maximum Depth of Binary Tree.
Memory Usage: 19 MB, less than 100.00% of C++ online submissions for Maximum Depth of Binary Tree.
# 堆栈实现DFS
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
    int maxDepth(TreeNode* root) {
        if (root == NULL) return 0;
        stack<pair<TreeNode*, int>> s;
        int deep = 1;
        s.push(pair<TreeNode*, int>(root, deep));
        while(!s.empty()){
            TreeNode* curNode = s.top().first;
            int curDeep = s.top().second;
            s.pop();
            if (curNode){
                deep = max(deep, curDeep);
                s.push(pair<TreeNode*, int>(curNode -> left, curDeep+1));
                s.push(pair<TreeNode*, int>(curNode -> right, curDeep+1));
            }
        }
        return deep;
    }
};
```
Runtime: 8 ms, faster than 87.69% of C++ online submissions for Maximum Depth of Binary Tree.
Memory Usage: 19.2 MB, less than 90.11% of C++ online submissions for Maximum Depth of Binary Tree.
# 知识总结

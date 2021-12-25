---
title: 257.Binary Tree Path
tags:
  - leetcode
  - tree
  - 深度优先
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 2991780344
date: 2020-09-04 14:45:46
---
# 题目描述
Given a binary tree, return all root-to-leaf paths.

Note: A leaf is a node with no children.

Example:
Input:

   1
 /   \
2     3
 \
  5

Output: ["1->2->5", "1->3"]
Explanation: All root-to-leaf paths are: 1->2->5, 1->3
# 我的解法
## 解题思路
返回所有二叉树的路径。一个路径的终点是叶节点，即它没有子节点。使用递归的方法，先判断当前节点是不是叶结点，如果是就把当前路径加入到返回数组中；如果不是，就进入它的子节点中。
## 实现代码
```C++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<string> res;
    void getPath(TreeNode* node, string s){
        s += to_string(node -> val);
        if (node -> left == nullptr && node -> right == nullptr){
            res.push_back(s);
            return;
        }
        s += "->";
        if (node -> left != nullptr) getPath(node -> left, s);
        if (node -> right!= nullptr) getPath(node -> right,s);
    }
    vector<string> binaryTreePaths(TreeNode* root) {
        if (root == nullptr)
            return res;
        getPath(root, "");
        return res;
    }
};
```
Runtime: 4 ms, faster than 87.67% of C++ online submissions for Binary Tree Paths.
Memory Usage: 13.9 MB, less than 46.20% of C++ online submissions for Binary Tree
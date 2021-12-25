---
title: 108.Convert Sorted Array to Binary Search Tree
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 137445652
date: 2020-03-06 19:49:46
---
# 题目描述
Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.

Example:
Given the sorted array: [-10,-3,0,5,9],
One possible answer is: [0,-3,9,-10,null,5], which represents the following height balanced BST:

      0
     / \
   -3   9
   /   /
 -10  5



# 我的解法
## 解题思路
复习下二叉搜索树🌲的概念：

一个二叉搜索树要满足以下特征：
* 每个元素有一个关键字，并且任意两个关键字都不同；因此，所有的关键字都是唯一的。
* 在根节点的左子树中，元素的关键字（如有）都小于根节点的关键字。
* 在根节点的右子树中，元素的关键字（如有）都大于根节点的关键字。
* 根节点的左、右子树也都是二叉搜索树。

使用递归的方法，每次将数组一分为2，记录中点为middle，将middle设置为root节点，左子树用数组\[begin，middle)来构成，右子树用\[middle+1,end)来构成，数组大小为0就返回nullptr，数组大小为1就返回关键字为这个数字的树节点。

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
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        if (nums.size() == 0) return nullptr;
        if (nums.size() == 1) return new TreeNode(nums[0]);
        
        int middle = nums.size() / 2;
        TreeNode* root = new TreeNode(nums[middle]);
        
        vector<int> left(nums.begin(), nums.begin() + middle);
        vector<int> right(nums.begin() + middle + 1, nums.end());

        root -> left = sortedArrayToBST(left);
        root -> right = sortedArrayToBST(right);

        return root;
    }
};
```

Runtime: 28 ms, faster than 54.42% of C++ online submissions for Convert Sorted Array to Binary Search Tree.
Memory Usage: 27.3 MB, less than 13.51% of C++ online submissions for Convert Sorted Array to Binary Search Tree.


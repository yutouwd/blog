---
title: 路径总和 1&2&3
tags:
  - leetcode
  - tree
  - 深度优先
  - 回溯法
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 171992954
date: 2021-09-28 16:51:46
---
# 路径总和1
## 题目描述

给你二叉树的根节点 root 和一个表示目标和的整数 targetSum ，判断该树中是否存在 根节点到叶子节点 的路径，这条路径上所有节点值相加等于目标和 targetSum 。
叶子节点 是指没有子节点的节点。

示例 1：
输入：root = [5,4,8,11,null,13,4,7,2,null,null,null,1], targetSum = 22
输出：true

示例 2：
输入：root = [1,2,3], targetSum = 5
输出：false

示例 3：
输入：root = [1,2], targetSum = 0
输出：false
 
提示：
树中节点的数目在范围 [0, 5000] 内
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000

## 解题思路
深度优先搜索，递归版
```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        if (root == nullptr)
            return false;
        if (root -> left == nullptr && root -> right == nullptr)
            return targetSum - root -> val == 0;
        return hasPathSum(root -> left, targetSum - root -> val) || hasPathSum(root -> right, targetSum - root -> val);
    }
};
```

迭代版，使用栈来记录节点和当前路径的和。

```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int targetSum) {
        if (!root) return false;
        stack<pair<TreeNode*, int>> s;
        s.push(make_pair(root, root -> val));
        int curr = 0;
        while(!s.empty()){
            auto t = s.top();
            s.pop();
            if (t.first -> right){
                s.push(make_pair(t.first -> right, t.second + t.first -> right -> val));
            }
            if (t.first -> left){
                s.push(make_pair(t.first -> left, t.second + t.first -> left -> val));
            }
            if (t.first->left == nullptr && t.first->right == nullptr && t.second==targetSum)
                return true;
        }
        return false;
    }
};
```

# 路径总和2
## 题目描述
给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

叶子节点 是指没有子节点的节点。

示例 1：
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]

示例 2：
输入：root = [1,2,3], targetSum = 5
输出：[]

示例 3：
输入：root = [1,2], targetSum = 0
输出：[]
 

提示：
树中节点总数在范围 [0, 5000] 内
-1000 <= Node.val <= 1000
-1000 <= targetSum <= 1000

## 解题思路
深度优先递归，感觉可以看成是回溯法。

```C++
class Solution {
public:
    vector<vector<int>> res;
    vector<int> vec;
    void dfs(TreeNode* node, int targetSum){
        if (node == nullptr)
            return;
        vec.push_back(node -> val);
        if (targetSum - node -> val == 0 && node->left == nullptr && node->right==nullptr){
            res.push_back(vec);
        }
        if (node-> left) dfs(node-> left, targetSum - node->val);
        if (node->right) dfs(node->right, targetSum - node->val);
        vec.pop_back();
        return;
    }
    vector<vector<int>> pathSum(TreeNode* root, int targetSum) {
        dfs(root,targetSum);
        return res;
    }
};
```
# 路径总和3
## 题目描述
给定一个二叉树的根节点 root ，和一个整数 targetSum ，求该二叉树里节点值之和等于 targetSum 的 路径 的数目。
路径 不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。

示例 1：
输入：root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
输出：3
解释：和等于 8 的路径有 3 条，如图所示。

示例 2：
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：3


提示:
二叉树的节点个数的范围是 [0,1000]
-109 <= Node.val <= 109 
-1000 <= targetSum <= 1000 

## 解题思路
路径不需要一定从根节点开始。


```C++
class Solution {
private:
    unordered_map<int, int> m;
public:
    int dfs(TreeNode* root, long long curr, int targetSum){
        if (!root)
            return 0;
        int ret = 0;
        curr += root -> val;
        if (m.count(curr - targetSum))
            ret = m[curr - targetSum];

        m[curr]++;
        ret += dfs(root -> left, curr, targetSum);
        ret += dfs(root -> right,curr, targetSum);
        m[curr]--;
        return ret;
    }
    
    int pathSum(TreeNode* root, int targetSum) {
        m[0] = 1;
        return dfs(root, 0, targetSum);
    }
};
```
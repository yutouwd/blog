---
title: 590.N-ary Tree Postorder Traversal
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2778829074
date: 2020-02-13 17:28:47
---
# 题目描述

# 我的解法
## 解题思路
### 递归
树的后序遍历，递归的方法和前序的类似，只不过需要调换下递归调用的顺序
```C++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
public:
    void postorder_traverse(vector<int>& nums, Node* tree_node){
        for (auto iter : tree_node -> children)
            postorder_traverse(nums, iter);
        nums.push_back(tree_node -> val);
    }
    vector<int> postorder(Node* root) {
        vector<int> nums;
        if (root == NULL) return nums;
        postorder_traverse(nums, root);
        return nums;
    }
};
```


Runtime: 100 ms, faster than 12.21% of C++ online submissions for N-ary Tree Postorder Traversal.
Memory Usage: 56.7 MB, less than 20.00% of C++ online submissions for N-ary Tree Postorder Traversal.


### 迭代
迭代的方法也和前序的类似，不过for的时候是要从前到后，因为最后的时候要把整个数组翻转过来，所以要让右边的最先pop出来。

```C++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/
class Solution {
public:
    vector<int> postorder(Node* root) {
        vector<int> nums;
        if (root == NULL) return nums;
        stack<Node*> s;
        s.push(root);
        while(!s.empty()){
            Node* tmp = s.top();
            s.pop();
            nums.push_back(tmp -> val);
            for (int i = 0; i < tmp -> children.size(); i++)
                s.push(tmp -> children[i]);
        }
        reverse(nums.begin(), nums.end());
        return nums;
    }
};
```


Runtime: 60 ms, faster than 84.99% of C++ online submissions for N-ary Tree Postorder Traversal.
Memory Usage: 56.5 MB, less than 20.00% of C++ online submissions for N-ary Tree Postorder Traversal.

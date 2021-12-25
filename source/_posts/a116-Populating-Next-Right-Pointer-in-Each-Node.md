---
title: 116.Populating Next Right Pointer in Each Node
tags:
  - leetcode
  - tree
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 3551767496
date: 2021-01-11 18:15:32
---
# 题目描述
You are given a perfect binary tree where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to NULL.

Initially, all next pointers are set to NULL.

 

Follow up:

You may only use constant extra space.
Recursive approach is fine, you may assume implicit stack space does not count as extra space for this problem.

# 我的解法
## 解题思路
使用一个队列来记录一层的节点。
## 实现代码
```C++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        Node* ret = root;
        if (root == nullptr) return ret;
        queue<Node*> q;
        q.push(root);
        while(!q.empty()){
            int n = q.size();
            for (int i = 0; i < n - 1; i++){
                Node* tmp =  q.front();
                q.pop();
                tmp -> next = q.front();
                if (tmp -> left) q.push(tmp -> left);
                if (tmp -> right)q.push(tmp -> right);
            }
            Node* tmp = q.front();
            q.pop();
            tmp -> next = nullptr;
            if (tmp -> left) q.push(tmp -> left);
            if (tmp -> right)q.push(tmp -> right);
        }
        return ret;
    }
};
```

不过这样使用的空间就有O(n)了，并不是常量空间。可以用递归的方法就不需要额外的空间。

```C++
class Solution {
public:
    Node* connect(Node* root) {
        if (root == NULL) return NULL;
        if (root -> left){
            root -> left -> next = root -> right;
            if (root -> right && root -> next){
                root -> right -> next = root -> next -> left;
            }
        }
        connect(root -> left);
        connect(root -> right);
        return root;
    }
};
```
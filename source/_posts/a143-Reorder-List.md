---
title: 143.Reorder List
tags:
  - leetcode
  - list
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 286346543
date: 2020-10-20 15:26:59
---
# 题目描述
Given a singly linked list L: L0→L1→…→Ln-1→Ln,
reorder it to: L0→Ln→L1→Ln-1→L2→Ln-2→…

You may not modify the values in the list's nodes, only nodes itself may be changed.

Example 1:
Given 1->2->3->4, reorder it to 1->4->2->3.

Example 2:
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.

# 我的解法
## 解题思路
将一个链表重新排序成：L0→Ln→L1→Ln-1→L2→Ln-2→…
最先想到的方法就是使用一个双向队列，将链表全部先都储存到双向队列中，然后再从前面取一个，后面取一个不断循环。
## 实现代码
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    void reorderList(ListNode* head) {
        if (head == nullptr) return;
        deque<ListNode*> q;
        ListNode* node = head;
        while (node){
            q.push_back(node);
            node = node -> next;
        }
        ListNode* dummyhead = new ListNode(0);
        node = dummyhead;
        while(!q.empty()){
            node -> next = q.front();
            node = node -> next;
            q.pop_front();
            if (!q.empty()){
                node -> next = q.back();
                node = node -> next;
                q.pop_back();
            }
        }
        node -> next = nullptr;
    }
};
```
执行用时：76 ms, 在所有 C++ 提交中击败了21.30%的用户
内存消耗：18.5 MB, 在所有 C++ 提交中击败了6.97%的用户
# 高票解法
其实用数组可能速度会更快
## 实现代码
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    void reorderList(ListNode* head) {
        vector<ListNode*> vec;
        ListNode* node = head;
        while(node){
            vec.push_back(node);
            node = node -> next;
        }
        int i = 0, j = vec.size() - 1;
        ListNode* dummyHead = new ListNode(0);
        node = dummyHead;
        while (i <= j){
            node -> next = vec[i++];
            node = node -> next;
            node -> next = vec[j--];
            node = node -> next;
        }
        node -> next = nullptr;
    }
};
```
执行用时：68 ms, 在所有 C++ 提交中击败了31.46%的用户
内存消耗：19 MB, 在所有 C++ 提交中击败了5.05%的用户
还是差不多
---
title: 21.Merge Two Sorted Lists
tags:
  - leetcode
  - list
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2341614181
date: 2019-09-07 11:23:23
---
# 题目描述
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

Example:

Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
# 我的解法
## 实现代码
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* head = new ListNode(0);
        ListNode* tail = head;
        
        while(l1 && l2){
            if (l1 -> val < l2 -> val){
                tail -> next = l1;
                l1 = l1 -> next;
            }
            else{
                tail -> next = l2;
                l2 = l2 -> next;
            }
            tail = tail -> next;
        }
        
        tail -> next = l1 ? l1 : l2;
        return head -> next;
    }
};

```

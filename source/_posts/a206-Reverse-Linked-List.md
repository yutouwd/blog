---
title: 206.Reverse Linked List
tags:
  - leetcode
  - list
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2829474180
date: 2019-09-17 10:59:26
---
# 题目描述
Reverse a singly linked list.

Example:
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL

Follow up:
A linked list can be reversed either iteratively or recursively. Could you implement both?

# 我的解法
## 解题思路
将一个链表反转过来

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
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = NULL;
        ListNode* cur = head;
        while (cur){
            ListNode* tmp = cur -> next;
            cur -> next = pre;
            pre = cur;
            cur = tmp;
        }
        return pre;
    }
};
```
Runtime: 8 ms, faster than 77.15% of C++ online submissions for Reverse Linked List.
Memory Usage: 9.3 MB, less than 77.10% of C++ online submissions for Reverse Linked List.

# 递归法
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
    ListNode* reverseList(ListNode* head) {
        if (head == NULL || head -> next == NULL) return head;
        ListNode* p = reverseList(head -> next);
        head -> next -> next = head;
        head -> next = NULL;
        return p;
    }
};
```
Runtime: 8 ms, faster than 77.11% of C++ online submissions for Reverse Linked List.
Memory Usage: 9.2 MB, less than 96.95% of C++ online submissions for Reverse Linked 

## 代码分析
递归法感觉挺难理解的

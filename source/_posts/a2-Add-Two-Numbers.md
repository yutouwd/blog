---
title: 2.Add Two Numbers
tags:
  - leetcode
  - list
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 2010047615
date: 2020-01-08 00:23:41
---
# 题目描述
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Example:

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
# 我的解法
## 实现代码
```C++
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummyhead = new ListNode(0);
        ListNode* p1 = dummyhead;
        int x = 0, y = 0, carry = 0;
        while (l1 || l2){
            if (l1){
                x = l1 -> val;
                l1 = l1 -> next;
            } 
            else
                x = 0;
            if (l2){
                y = l2 -> val;
                l2 = l2 -> next;
            }
            else
                y = 0;
            p1 -> next = new ListNode((x + y + carry) % 10);
            carry = x + y >= 10 ? 1 : 0;
            p1 = p1 -> next;
        }
        if (carry)
            p1 -> next = new ListNode(1);
        return dummyhead -> next;
    }
};
```

可以写得更简洁一些：
```C++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int cur = 0;
        ListNode* dummyHead = new ListNode(0);
        ListNode* p = dummyHead;
        while (cur || l1 || l2){
            if (l1){
                cur += l1 -> val;
                l1 = l1 -> next;
            }
            if (l2){
                cur += l2 -> val;
                l2 = l2 -> next;
            }
            p -> next = new ListNode(cur % 10);
            p = p -> next;
            cur /= 10;
        }
        if (cur)
            p -> next = new ListNode(1);
        return dummyHead -> next;
    }
};
```
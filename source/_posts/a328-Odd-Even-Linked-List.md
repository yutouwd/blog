---
title: 328.Odd Even Linked List
tags:
  - leetcode
  - list
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 1942160452
date: 2020-12-18 00:25:20
---
# 题目描述
Given a singly linked list, group all odd nodes together followed by the even nodes. Please note here we are talking about the node number and not the value in the nodes.

You should try to do it in place. The program should run in O(1) space complexity and O(nodes) time complexity.

Example 1:
Input: 1->2->3->4->5->NULL
Output: 1->3->5->2->4->NULL

Example 2:
Input: 2->1->3->5->6->4->7->NULL
Output: 2->3->6->7->1->5->4->NULL

Constraints:
The relative order inside both the even and odd groups should remain as it was in the input.
The first node is considered odd, the second node even and so on ...
The length of the linked list is between [0, 10^4].

# 我的解法
## 解题思路
将链表的奇数节点放到前面，偶数节点放到后面，使用原地算法。
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
    ListNode* oddEvenList(ListNode* head) {
        if (head == nullptr) return head;
        ListNode* evenHead = new ListNode(0);
        ListNode* odd = head;      // 记录奇数节点
        ListNode* eve = evenHead;  // 记录偶数节点
        while(odd && odd -> next){ // 到了链表的尾端
            eve -> next = odd -> next;
            eve = eve -> next;
            // 链表分为两种情况，有奇数个节点或者偶数个节点
            if (odd -> next -> next){ // 未到尾端或者有奇数个节点（在while判断出跳出）
                odd -> next = odd -> next -> next;
                odd = odd -> next;
            }
            else // 偶数个节点
                odd -> next = nullptr;
        }
        eve -> next = nullptr;
        odd -> next = evenHead -> next;
        return head;
    }
};
```

---
title: 876.Middle of the Linked List
tags:
  - leetcode
  - list
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 2202627585
date: 2020-04-14 19:39:37
---
# 题目描述
Given a non-empty, singly linked list with head node head, return a middle node of linked list.

If there are two middle nodes, return the second middle node.

Example 1:

Input: [1,2,3,4,5]
Output: Node 3 from this list (Serialization: [3,4,5])
The returned node has value 3.  (The judge's serialization of this node is [3,4,5]).
Note that we returned a ListNode object ans, such that:
ans.val = 3, ans.next.val = 4, ans.next.next.val = 5, and ans.next.next.next = NULL.

Example 2:
Input: [1,2,3,4,5,6]
Output: Node 4 from this list (Serialization: [4,5,6])
Since the list has two middle nodes with values 3 and 4, we return the second one.
 

Note:
The number of nodes in the given list will be between 1 and 100.

# 我的解法
## 解题思路
使用双指针，慢指针一次走一步，快指针一次走两步，当快指针走到了头的时候，慢指针就到了链表的中间。
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
    ListNode* middleNode(ListNode* head) {
        ListNode* p1 = head;
        ListNode* p2 = head;
        while(p2 && p2 -> next){
            p1 = p1 -> next;
            p2 = p2 -> next -> next;
        }
        return p1;
    }
};


```

执行用时 :0 ms, 在所有 C++ 提交中击败了100.00%的用户
内存消耗 :8 MB, 在所有 C++ 提交中击败了100.00%的用户

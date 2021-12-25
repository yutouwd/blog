---
title: 142.Linked List CycleII
tags:
  - leetcode
  - list
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 3693154351
date: 2020-01-07 23:21:08
---
# 题目描述
Given a linked list, return the node where the cycle begins. If there is no cycle, return null.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list.

Note: Do not modify the linked list.

Example 1:
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.


Example 2:
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.


Example 3:
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.

Follow-up:
Can you solve it without using extra space?
# 我的解法
## 解题思路
和上一题类似，使用set的方法比较容易想到。用一个set来记录已经遍历过的node，如果发现了有重复的，那么这个node就是环开始的地方。
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
    ListNode *detectCycle(ListNode *head) {
        set<ListNode*> s;
        ListNode* p = head;
        while(p){
            if (s.find(p) != s.end())
                return p;
            s.insert(p);
            p = p -> next;
        }
        return NULL;
    }
};
```

## 快慢指针
现在还不太理解
<https://leetcode.com/problems/linked-list-cycle-ii/discuss/44781/Concise-O(n)-solution-by-using-C%2B%2B-with-Detailed-Alogrithm-Description>
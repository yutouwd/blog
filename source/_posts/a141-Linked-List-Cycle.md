---
title: 141.Linked List Cycle
tags:
  - leetcode
  - list
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 3103972891
date: 2020-01-07 23:30:13
---
# 题目描述
Given a linked list, determine if it has a cycle in it.

To represent a cycle in the given linked list, we use an integer pos which represents the position (0-indexed) in the linked list where tail connects to. If pos is -1, then there is no cycle in the linked list. 

Example 1:
Input: head = [3,2,0,-4], pos = 1
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the second node.


Example 2:
Input: head = [1,2], pos = 0
Output: true
Explanation: There is a cycle in the linked list, where tail connects to the first node.


Example 3:
Input: head = [1], pos = -1
Output: false
Explanation: There is no cycle in the linked list.

# 我的解法
## 解题思路
一开始完全没有思路，看了下题解才发现其实可以用set来判断有没有出现重复的node

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
    bool hasCycle(ListNode *head) {
        set<ListNode*> s;
        ListNode* p = head;
        int pos = -1;
        while(p){
            if (s.find(p) != s.end()){
                pos++;
                return true;
            }
            s.insert(p);
            p = p -> next;
        }
        return false;
    }
};


```


Runtime: 20 ms, faster than 17.13% of C++ online submissions for Linked List Cycle.
Memory Usage: 12.2 MB, less than 10.53% of C++ online submissions for Linked List Cycle.

## 快慢指针
用两个指针，慢指针一次移动一步，快指针一次移动两步，然后判断快指针和慢指针会不会相等，如果相等则存在环。

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
    bool hasCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast && fast -> next){
            fast = fast -> next -> next;
            slow = slow -> next;
            if (fast == slow) return true;
        }
        return false;
    }
};

```


Runtime: 8 ms, faster than 97.20% of C++ online submissions for Linked List Cycle.
Memory Usage: 9.9 MB, less than 43.42% of C++ online submissions for Linked List Cycle.

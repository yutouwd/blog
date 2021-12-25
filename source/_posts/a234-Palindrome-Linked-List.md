---
title: 234.Palindrome Linked List
tags:
  - leetcode
  - list
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 3702077338
date: 2020-02-13 16:49:03
---
# 题目描述
Given a singly linked list, determine if it is a palindrome.

Example 1:
Input: 1->2
Output: false

Example 2:
Input: 1->2->2->1
Output: true

Follow up:
Could you do it in O(n) time and O(1) space?

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
    bool isPalindrome(ListNode* head) {
        if (!head || !(head -> next)) return true;
        int len = 0;
        ListNode* p1 = head;
        while(p1){
            len++;
            p1 = p1 -> next;
        }
        int n = len / 2;
        int mod = len % 2;
        ListNode* p2 = head;
        stack<int> s;
        for (int i = 0; i < n; i++){
            s.push(p2 -> val);
            p2 = p2 -> next;
        }
        if (mod)
            p2 = p2 -> next;
        for (int i = 0; i < n; i++){
            int tmp = s.top();
            s.pop();
            if (tmp != p2 -> val)
                return false;
            p2 = p2 -> next;
        }
        return true;
    }
};

```

Runtime: 16 ms, faster than 98.87% of C++ online submissions for Palindrome Linked List.
Memory Usage: 13.1 MB, less than 37.93% of C++ online submissions for Palindrome Linked List.
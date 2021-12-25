---
title: 445.Add Two Numbers II
tags:
  - leetcode
  - list
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 1819473222
date: 2020-04-14 19:43:49
---
# 题目描述
You are given two non-empty linked lists representing two non-negative integers. The most significant digit comes first and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

Follow up:
What if you cannot modify the input lists? In other words, reversing the lists is not allowed.

Example:

Input: (7 -> 2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 8 -> 0 -> 7

# 我的解法
## 解题思路
还是将两个链表加起来，链表的前面位代表的是数字的低位，想到的办法是先将链表转化成数字，然后再把两个数字加起来，但是发现会有很多数据类型的问题，因为链表的数字可能会比long long还要大。所以就把链表先转成string，然后再一位位的相加，最后转换成链表。
## 实现代码
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
        string str1, str2;
        while(l1){
            str1.push_back(to_string(l1 -> val)[0]);
            l1 = l1 -> next;
        }
        while(l2){
            str2.push_back(to_string(l2 -> val)[0]);
            l2 = l2 -> next;
        }
        int i = str1.size() - 1, j = str2.size() - 1, cur = 0;
        string ans;
        while (cur || i >= 0 || j >= 0){
            if (i >= 0) cur += str1[i--] - '0';
            if (j >= 0) cur += str2[j--] - '0';
            ans.push_back(to_string(cur % 10)[0]);
            cur /= 10;
        }
        ListNode* dummyHead = new ListNode(0);
        ListNode* p = dummyHead;
        for (int k = ans.size() - 1; k >= 0; k--){
            p -> next = new ListNode(ans[k] - '0');
            p = p -> next;
        }
        return dummyHead -> next;
    }
};


```

Runtime: 44 ms, faster than 8.73% of C++ online submissions for Add Two Numbers II.
Memory Usage: 9.8 MB, less than 100.00% of C++ online submissions for Add Two Numbers II.

# 高票解法
使用字符串转换的方法速度非常的慢，看了下题解，可以用栈来完成。最后将栈一位位pop出来相加，并反向构造一个链表
## 实现代码
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
        stack<int> s1, s2;
        while(l1){
            s1.push(l1 -> val);
            l1 = l1 -> next;
        }
        while(l2){
            s2.push(l2 -> val);
            l2 = l2 -> next;
        }
        int cur = 0;
        ListNode* curNode = nullptr;
        ListNode* ansNode = nullptr;
        while (cur || !s1.empty() || !s2.empty()){
            if (!s1.empty()){
                cur += s1.top();
                s1.pop();
            }
            if (!s2.empty()){
                cur += s2.top();
                s2.pop();
            }
            ansNode = new ListNode(cur % 10);
            ansNode -> next = curNode;
            curNode = ansNode;  
            cur /= 10;
        }
        return ansNode;
    }
};


```
Runtime: 32 ms, faster than 59.39% of C++ online submissions for Add Two Numbers II.
Memory Usage: 12.1 MB, less than 51.85% of C++ online submissions for Add Two Numbers II.
---
title: 19.Remove Nth Node From End of List
tags:
  - leetcode
  - list
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 1165746741
date: 2019-09-05 16:44:18
---
# 题目描述
Given a linked list, remove the n-th node from the end of list and return its head.

Example:

Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
Note:

Given n will always be valid.

Follow up:

Could you do this in one pass?


# 我的解法
## 解题思路
想到的办法是先遍历一次链表，求出链表的长度，再删除对应的节点。
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (!head || !(head -> next)) return NULL; //如果链表为空或者只有一个节点返回NULL
        /*先求链表长度*/
        ListNode* p1 = head;
        int len = 0;
        while(p1){
            len++;
            p1 = p1 -> next;
        }
        /*删除节点*/
        ListNode* p2 = head; //用于删除节点
        ListNode* p3 = head; //用于记录head位置，最后返回
        if (len == n){       //如果是删除第一个节点
            p2 = p2 -> next;
            return p2;
        }
        for (int i = 0; i < len - n - 1; i++) //移动到要删除的节点之前
            p2 = p2 -> next;
        p2 -> next = p2 -> next -> next;
        return p3;
    }
};
```

Runtime: 4 ms, faster than 85.75% of C++ online submissions for Remove Nth Node From End of List.
Memory Usage: 8.6 MB, less than 67.11% of C++ online submissions for Remove Nth Node From End of List.

# 高票解法
看了下题解才知道怎么只用一次遍历就能完成，思路是：
设置两个指针p和q，当p指向链表的末尾NULL时，p和q之间间隔的元素为n，删掉p下一个节点就可以了
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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (!head || !(head -> next)) return NULL;
        ListNode* dummyHead = new ListNode(0);
        dummyHead -> next = head;
        ListNode* first = dummyHead;
        ListNode* second= dummyHead;
        for (int i = 0; i < n + 1; i++)
            first = first -> next;
        while(first){
            first = first -> next;
            second= second-> next;
        }
        second -> next = second -> next -> next;
        return dummyHead -> next;
    }
};
```
## 代码分析

其实不太理解为什么都要用到dummyHead，它的next指向head。但如果不用的话就会出现各种边界问题。看了下一个动画图解和评论，好像有点理解了。因为要找的是待删除结点的前一个节点，而头结点没有前一个节点，所以设置了一个虚拟节点

# 知识总结
链表的节点删除
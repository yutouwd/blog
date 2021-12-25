---
title: 725.Split LinkedList in Parts
tags:
  - leetcode
  - list
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 3339355851
date: 2021-09-22 15:59:56
---
# 题目描述
给你一个头结点为 head 的单链表和一个整数 k ，请你设计一个算法将链表分隔为 k 个连续的部分。
每部分的长度应该尽可能的相等：任意两部分的长度差距不能超过 1 。这可能会导致有些部分为 null 。
这 k 个部分应该按照在链表中出现的顺序排列，并且排在前面的部分的长度应该大于或等于排在后面的长度。
返回一个由上述 k 部分组成的数组。

 
示例 1：
输入：head = [1,2,3], k = 5
输出：[[1],[2],[3],[],[]]
解释：
第一个元素 output[0] 为 output[0].val = 1 ，output[0].next = null 。
最后一个元素 output[4] 为 null ，但它作为 ListNode 的字符串表示是 [] 。

示例 2：
输入：head = [1,2,3,4,5,6,7,8,9,10], k = 3
输出：[[1,2,3,4],[5,6,7],[8,9,10]]
解释：
输入被分成了几个连续的部分，并且每部分的长度相差不超过 1 。前面部分的长度大于等于后面部分的长度。
 

提示：

链表中节点的数目在范围 [0, 1000]
0 <= Node.val <= 1000
1 <= k <= 50

# 我的解法
## 解题思路
一开始想着分成len小于等于k和大于k两种情况，但是看题解发现，其实并不需要分成这两种情况。
## 实现代码
```C++
class Solution {
public:
    vector<ListNode*> splitListToParts(ListNode* head, int k) {
        ListNode* p = head;
        int len = 0;
        while(p){
            p = p -> next;
            len++;
        }
        vector<ListNode*> res;
        p = head;
        if (len <= k){
            for (int i = 0; i < len; i++){
                ListNode* tmp = p -> next;
                p -> next = nullptr;
                res.push_back(p);
                p = tmp;
            }
            for (int i = 0; i < k-len; i++)
                res.push_back(nullptr);
        }
        else{
            int div = len / k, mod = len % k;
            int n = 0;
            for (int i = 0; i < k; i++){
                ListNode* t = p;
                for (int j = 0; j < div-1; j++)
                    t = t -> next;
                if (n < mod){
                    n++;
                    t = t -> next;
                }
                ListNode* tmp = t -> next;
                t -> next = nullptr;
                res.push_back(p);
                p = tmp;
            }
        }


        return res;
    }
};

```
# 高票解法
## 实现代码
题解写得还是简洁多了。
```C++
class Solution {
public:
    vector<ListNode*> splitListToParts(ListNode* head, int k) {
        int n = 0;
        ListNode *temp = head;
        while (temp != nullptr) {
            n++;
            temp = temp->next;
        }
        int quotient = n / k, remainder = n % k;

        vector<ListNode*> parts(k,nullptr);
        ListNode *curr = head;
        for (int i = 0; i < k && curr != nullptr; i++) {
            parts[i] = curr;
            int partSize = quotient + (i < remainder ? 1 : 0);
            for (int j = 1; j < partSize; j++) {
                curr = curr->next;
            }
            ListNode *next = curr->next;
            curr->next = nullptr;
            curr = next;
        }
        return parts;
    }
};


```
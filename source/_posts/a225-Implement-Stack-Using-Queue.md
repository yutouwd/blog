---
title: 225.Implement Stack Using Queue
tags:
  - leetcode
  - design
  - stack
  - queue
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 619958913
date: 2020-03-01 16:05:29
---
# 题目描述
现在leetcode有了每天打卡活动，正好可以做一做自己平时看了觉得太难不想做的题，顺便积累积累积分，想靠参加周赛得积分对我来说可太难了。

Implement the following operations of a stack using queues.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
empty() -- Return whether the stack is empty.

Example:
MyStack stack = new MyStack();
stack.push(1);
stack.push(2);  
stack.top();   // returns 2
stack.pop();   // returns 2
stack.empty(); // returns false

Notes:
You must use only standard operations of a queue -- which means only push to back, peek/pop from front, size, and is empty operations are valid.
Depending on your language, queue may not be supported natively. You may simulate a queue by using a list or deque (double-ended queue), as long as you use only standard operations of a queue.
You may assume that all operations are valid (for example, no pop or top operations will be called on an empty stack).

# 我的解法
## 解题思路
用队列来实现一个栈，对于这种设计问题一直都不太会做，参考了<https://leetcode.com/problems/implement-stack-using-queues/discuss/62527/A-simple-C%2B%2B-solution>

用一个队列完成，在push进去的时候，先把要push的元素推进队列，然后循环n-1次把队列最前面的push到队列中然后在pop出来。这样就相当于把每次push进去元素到放到了队列到最前面，pop的时候就最先把队列的最前面给pop出来。相当于实现了栈的先进后出。


## 实现代码
```C++
class MyStack {
public:
    /** Initialize your data structure here. */
    queue<int> q;
    MyStack() {

    }
    
    /** Push element x onto stack. */
    void push(int x) {
        q.push(x);
        for (int i = 0; i < q.size() - 1; i++){
            q.push(q.front());
            q.pop();
        }
    }
    
    /** Removes the element on top of the stack and returns that element. */
    int pop() {
        int ret = q.front();
        q.pop();
        return ret;
    }
    
    /** Get the top element. */
    int top() {
        return q.front();
    }
    
    /** Returns whether the stack is empty. */
    bool empty() {
        return q.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */

```
Runtime: 0 ms, faster than 100.00% of C++ online submissions for Implement Stack using Queues.
Memory Usage: 8.1 MB, less than 100.00% of C++ online submissions for Implement Stack using Queues.

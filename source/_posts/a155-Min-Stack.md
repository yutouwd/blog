---
title: 155.Min Stack
tags:
  - leetcode
  - design
  - stack
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 2122295331
date: 2020-03-03 15:50:41
---
# 题目描述
Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

push(x) -- Push element x onto stack.
pop() -- Removes the element on top of the stack.
top() -- Get the top element.
getMin() -- Retrieve the minimum element in the stack.
 

Example:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
# 我的解法
## 解题思路
设计一个最小栈，依旧是不太会做的设计题目。下面的解法参考了一些高票解法。
## 两个栈
用两个栈，s1记录全部push进去的，s2记录当前的最小值。在push的时候，先把x push到s1中，然后判断x是不是最小的数。如果是最小的数就再push到s2中。在pop的时候先判断s1最上面的是不是最小值，是的话就s2也pop一次。

```C++

class MinStack {
private:
stack<int> s1;
stack<int> s2;  // minstack
public:
    /** initialize your data structure here. */
    MinStack() {
    }
    
    void push(int x) {
        s1.push(x);
        if (s2.empty() || x <= s2.top())
            s2.push(x);
    }
    
    void pop() {
        if (s1.top() == s2.top()){
            s1.pop();
            s2.pop();
        }
        else
            s1.pop();
    }
    
    int top() {
        return s1.top();
    }
    
    int getMin() {
        return s2.top();
    }
};
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */


```

## 使用pair
用pair来作为栈的数据，第一个储存当前值，第二个储存最小值
```C++

class MinStack {
private:
stack<pair<int, int>> s;
public:
    /** initialize your data structure here. */
    MinStack() {
    }
    
    void push(int x) {
        int tmp;
        if (s.empty())
            tmp = x;
        else
            tmp = min(x, s.top().second);
        s.push({x, tmp});
    }
    
    void pop() {
        s.pop();
    }
    
    int top() {
        return s.top().first;
    }
    
    int getMin() {
        return s.top().second;
    }
};
/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */


```
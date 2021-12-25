---
title: 77.Combinations
tags:
  - leetcode
  - 回溯法
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 1059005173
date: 2020-09-08 15:14:12
---
# 题目描述
Given two integers n and k, return all possible combinations of k numbers out of 1 ... n.

You may return the answer in any order.

Example 1:
Input: n = 4, k = 2
Output:
[
  [2,4],
  [3,4],
  [2,3],
  [1,2],
  [1,3],
  [1,4],
]

Example 2:
Input: n = 1, k = 1
Output: [[1]]
 

Constraints:

1 <= n <= 20
1 <= k <= n

# 我的解法
## 解题思路
之前还没有怎么做过用回溯法的题目，现在学习一下。
参考<https://labuladong.gitbook.io/algo/suan-fa-si-wei-xi-lie/hui-su-suan-fa-xiang-jie-xiu-ding-ban>

解决回溯问题，其实就是一个决策树的遍历，需要思考三个问题：
1. 路径：也就是已经做出的选择。
2. 选择列表：也就是你当前可以做的选择。
3. 结束条件：也就是到达决策树底层，无法再做选择的条件。

解题的框架如下：
```python
result = []
def backtrack(路径, 选择列表):
    if 满足结束条件:
        result.add(路径)
        return

    for 选择 in 选择列表:
        做选择
        backtrack(路径, 选择列表)
        撤销选择
```

对于这道题而言，结束条件应该是当前选择当数组大小等于k；选择就应该是当前的值到n
## 实现代码
```C++
class Solution {
public:
    vector<vector<int>> res;
    vector<int> vec;
    void backtracking(int n, int k, int startIdx){
        if (vec.size() == k){
            res.push_back(vec);
            return;
        }

        for (int i = startIdx; i <= n; i++){
            vec.push_back(i);
            backtracking(n, k, i + 1);
            vec.pop_back();
        }
    }
    vector<vector<int>> combine(int n, int k) {
        backtracking(n, k, 1);
        return res;
    }
};
```
执行用时：40 ms, 在所有 C++ 提交中击败了74.90%的用户
内存消耗：10.4 MB, 在所有 C++ 提交中击败了29.53%的用户
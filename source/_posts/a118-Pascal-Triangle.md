---
title: 118.Pascal Triangle
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 281994477
date: 2019-09-26 13:21:10
---
# 题目描述
Given a non-negative integer numRows, generate the first numRows of Pascal's triangle.


In Pascal's triangle, each number is the sum of the two numbers directly above it.

Example:
Input: 5
Output:
[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]

# 我的解法
## 实现代码
这题比较简单
```C++
class Solution {
public:
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ans;
        ans.resize(numRows);
        for (int i = 0; i < numRows; i++){
            ans[i].resize(i + 1);
            for (int j = 0; j < i + 1; j++){
                if (j == 0 || j == i)
                    ans[i][j] = 1;
                else
                    ans[i][j] = ans[i-1][j-1] + ans[i-1][j];
            }
        }
        return ans;
    }
};
```

Runtime: 4 ms, faster than 60.45% of C++ online submissions for Pascal's Triangle.
Memory Usage: 8.8 MB, less than 88.89% of C++ online submissions for Pascal's Triangle.
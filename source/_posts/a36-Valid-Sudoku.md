---
title: 36.Valid Sudoku
tags:
  - leetcode
  - vector
categories:
  - leetcode
  - medium
copyright: true
comments: true
notshow: true
abbrlink: 2138873447
date: 2019-12-19 23:48:12
---
# 题目描述
Determine if a 9x9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:

Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the 9 3x3 sub-boxes of the grid must contain the digits 1-9 without repetition.

A partially filled sudoku which is valid.

The Sudoku board could be partially filled, where empty cells are filled with the character '.'.

Example 1:
Input:
[
  ["5","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: true

Example 2:
Input:
[
  ["8","3",".",".","7",".",".",".","."],
  ["6",".",".","1","9","5",".",".","."],
  [".","9","8",".",".",".",".","6","."],
  ["8",".",".",".","6",".",".",".","3"],
  ["4",".",".","8",".","3",".",".","1"],
  ["7",".",".",".","2",".",".",".","6"],
  [".","6",".",".",".",".","2","8","."],
  [".",".",".","4","1","9",".",".","5"],
  [".",".",".",".","8",".",".","7","9"]
]
Output: false
Explanation: Same as Example 1, except with the 5 in the top left corner being 
    modified to 8. Since there are two 8's in the top left 3x3 sub-box, it is invalid.

Note:
A Sudoku board (partially filled) could be valid but is not necessarily solvable.
Only the filled cells need to be validated according to the mentioned rules.
The given board contain only digits 1-9 and the character '.'.
The given board size is always 9x9.
# 我的解法
## 解题思路
判断一个数独是不是有效的，只要检查同一行同一列和同一个3x3的格子有没有重复的数字。
## 实现代码
```C++
class Solution {
public:
    bool CheckValid(vector<char>& vec){
        if (vec.size() == 0)
            return true;
        unordered_map<char, int> count;
        for (char i : vec){
            count[i]++;
        }
        for (auto iter = count.begin(); iter != count.end(); iter++){
            if (iter -> second > 1)
                return false;
        }
        return true;
    }
    bool isValidSudoku(vector<vector<char>>& board) {
        bool validRow = true, validCol = true, validBlk = true;
        //check row
        vector<char> check;
        for (int i = 0; i < 9; i++){
            for (int j = 0; j < 9; j++){
                if (board[i][j] != '.')
                    check.push_back(board[i][j]);
            }
            bool tmp = CheckValid(check);
            validRow = tmp && validRow;
            check.clear();
        }
        //check column
        for (int i = 0; i < 9; i++){
            for (int j = 0; j < 9; j++){
                if (board[j][i] != '.')
                    check.push_back(board[j][i]);
            }
            bool tmp = CheckValid(check);
            validCol = tmp && validCol;
            check.clear();
        }
        //check block
        for (int i = 0; i < 9; i += 3){
            for (int j = 0; j < 9; j += 3){
                for (int k = 0; k < 3; k++){
                    for (int l = 0; l < 3; l++){
                        if (board[i+k][j+l] != '.')
                            check.push_back(board[i+k][j+l]);
                    }
                }
                bool tmp = CheckValid(check);
                validBlk = tmp && validBlk;
                check.clear();
            }
        }
        return validRow && validCol && validBlk;
    }
};
```
Runtime: 24 ms, faster than 15.59% of C++ online submissions for Valid Sudoku.
Memory Usage: 11.9 MB, less than 20.51% of C++ online submissions for Valid Sudoku.
# 高票解法
速度很慢，还要看下高票解法是怎么做的。
## 实现代码
每日一题做到了两年前做过的一道。

```C++
class Solution {
public:
    bool isValidSudoku(vector<vector<char>>& board) {
        int row[9][9];
        int col[9][9];
        int sub[3][3][9];

        memset(row, 0, sizeof(row));
        memset(col, 0, sizeof(col));
        memset(sub, 0, sizeof(col));
        for (int i = 0; i < 9; i++){
            for (int j = 0; j < 9; j++){
                char c = board[i][j];
                if (c != '.'){
                    int idx = c - '1';
                    row[i][idx]++;
                    col[j][idx]++;
                    sub[i/3][j/3][idx]++;
                    if (row[i][idx]>1 || col[j][idx] > 1 || sub[i/3][j/3][idx]>1)
                        return false;
                }
            }
        }
        return true;
    }
};
```
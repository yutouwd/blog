---
title: 130.Surrounded Regions
tags:
  - leetcode
  - 深度优先
  - 广度优先
categories:
  - leetcode
  - medium
copyright: true
comments: true
abbrlink: 172704068
date: 2020-08-11 23:06:06
---
# 题目描述
Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.

A region is captured by flipping all 'O's into 'X's in that surrounded region.

Example:
X X X X
X O O X
X X O X
X O X X

After running your function, the board should be:
X X X X
X X X X
X X X X
X O X X

Explanation:
Surrounded regions shouldn’t be on the border, which means that any 'O' on the border of the board are not flipped to 'X'. Any 'O' that is not on the border and it is not connected to an 'O' on the border will be flipped to 'X'. Two cells are connected if they are adjacent cells connected horizontally or vertically.
# 深度优先
## 解题思路
如果一个O没有被包围，那么他一定会和一个边上的O相连，所以就从边上的O开始深度优先搜索并标记下来相连的O。
## 实现代码
```C++
class Solution {
public:
    int n, m;
    void dfs(vector<vector<char>>& board, int x, int y){
        if (x < 0 || x >= n || y < 0 || y >= m || board[x][y] != 'O')
            return;
        board[x][y] = '-';
        dfs(board, x, y-1);
        dfs(board, x, y+1);
        dfs(board, x-1, y);
        dfs(board, x+1, y);
    }
    void solve(vector<vector<char>>& board) {
        if (board.size() == 0) return;
        n = board.size();
        m = board[0].size();
        for (int i = 0; i < n; i++){
            dfs(board, i, 0);
            dfs(board, i, m-1);
        }
        for (int i = 0; i < m; i++){
            dfs(board, 0, i);
            dfs(board, n-1, i);
        }
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (board[i][j] == '-')
                    board[i][j] = 'O';
                else if (board[i][j] == 'O')
                    board[i][j] = 'X';
            }
        }
    }
};
```

Runtime: 28 ms, faster than 78.29% of C++ online submissions for Surrounded Regions.
Memory Usage: 10.2 MB, less than 71.02% of C++ online submissions for Surrounded Regions.

# 广度优先
## 解题思路
首先将边缘上的O加入队列，然后就开始遍历队列，将O改为标记符，然后再遍历当前的点的四领域，如果是O就加入队列。
## 实现代码
```C++
class Solution {
public:
    int xx[4] = {1 ,-1 ,0 ,0};
    int yy[4] = {0, 0, 1, -1};
    void solve(vector<vector<char>>& board) {
        if (board.size() == 0) return;
        int n = board.size(), m = board[0].size();
        queue<pair<int, int >> q;
        
        for (int i = 0; i < n; i++){
            if (board[i][0] == 'O')
                q.emplace(i, 0);
            if (board[i][m-1] == 'O')
                q.emplace(i, m-1);
        }
        
        for (int i = 1; i < m - 1; i++){
            if (board[0][i] == 'O')
                q.emplace(0, i);
            if (board[n-1][i] == 'O')
                q.emplace(n-1, i);
        }
        
        while(!q.empty()){
            int x = q.front().first, y = q.front().second;
            q.pop();
            board[x][y] = '-';
            for (int i = 0; i < 4; i++){
                int a = x + xx[i], b = y + yy[i];
                if (a < 0 || a >= n || b < 0 || b >= m || board[a][b] != 'O')
                    continue;
                q.emplace(a, b);
            }
        }
        
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (board[i][j] == '-')
                    board[i][j] = 'O';
                else if (board[i][j] == 'O')
                    board[i][j] = 'X';
            }
        }
    }
};
```
Runtime: 28 ms, faster than 78.29% of C++ online submissions for Surrounded Regions.
Memory Usage: 10.2 MB, less than 65.90% of C++ online submissions for Surrounded Regions.
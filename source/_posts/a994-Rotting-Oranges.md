---
title: 994.Rotting Oranges
tags:
  - leetcode
  - 广度优先
categories:
  - leetcode
copyright: true
comments: true
abbrlink: 1420042497
date: 2020-03-05 18:33:32
---
# 题目描述
In a given grid, each cell can have one of three values:

the value 0 representing an empty cell;
the value 1 representing a fresh orange;
the value 2 representing a rotten orange.
Every minute, any fresh orange that is adjacent (4-directionally) to a rotten orange becomes rotten.

Return the minimum number of minutes that must elapse until no cell has a fresh orange.  If this is impossible, return -1 instead.
 
Example 1:
Input: [[2,1,1],[1,1,0],[0,1,1]]
Output: 4

Example 2:
Input: [[2,1,1],[0,1,1],[1,0,1]]
Output: -1
Explanation:  The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.

Example 3:
Input: [[0,2]]
Output: 0
Explanation:  Since there are already no fresh oranges at minute 0, the answer is just 0.
 

Note:
1 <= grid.length <= 10
1 <= grid[0].length <= 10
grid[i][j] is only 0, 1, or 2.
# 我的解法
## 解题思路
比较直观的方法，先遍历数组一遍，计算出新鲜橘子和腐烂橘子的个数。并使用一个队列，将腐烂橘子的位置push进去。之后开始遍历这个队列，直到队列为空，每次遍历的次数为上一次队列的size（即使模拟一天橘子的腐烂），检查这些腐烂的橘子的周围有没有新鲜的橘子，有新鲜的橘子就把这给点加入到队列并改为腐烂的橘子。这里要注意的是，遍历队列到空其实会导致最后一次队列中都是腐烂的橘子并且周围没有可以改变的新鲜的橘子，所以要在循环中检查下一次队列的遍历有没有改变腐烂的橘子数，如果没有就要把天数减一。
## 实现代码

```C++

class Solution {
public:
    int orangesRotting(vector<vector<int>>& grid) {
        int n = grid.size(), m = grid[0].size();
        int numFresh = 0, numRotten = 0;
        queue<pair<int, int>> q;
        for (int i = 0; i < n; i++){
            for (int j = 0; j < m; j++){
                if (grid[i][j] == 1)
                    numFresh++;
                if (grid[i][j] == 2){
                    numRotten++;
                    q.push({i, j});
                }
            }
        }
        int time = 0;
        while(!q.empty()){
            time++;
            int queueSize = q.size();
            int lastRotten = numRotten;
            for (int i = 0; i < queueSize; i++){
                int x = q.front().first, y = q.front().second;
                q.pop();
                if (x - 1 >= 0 && grid[x-1][y] == 1){
                    q.push({x-1, y});
                    grid[x-1][y] = 2;
                    numFresh--;
                    numRotten++;
                }
                if (x + 1 < n && grid[x+1][y] == 1){
                    q.push({x+1, y});
                    grid[x+1][y] = 2;
                    numFresh--;
                    numRotten++;
                }
                if (y - 1 >= 0 && grid[x][y-1] == 1){
                    q.push({x, y-1});
                    grid[x][y-1] = 2;
                    numFresh--;
                    numRotten++;
                }
                if (y + 1 < m && grid[x][y+1] == 1){
                    q.push({x, y+1});
                    grid[x][y+1] = 2;
                    numFresh--;
                    numRotten++;
                }
            }
            if (lastRotten == numRotten)
                time--;
        }
        return (numFresh != 0) ? -1 : time;
    }
};


```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Rotting Oranges.
Memory Usage: 7.9 MB, less than 100.00% of C++ online submissions for Rotting Oranges.

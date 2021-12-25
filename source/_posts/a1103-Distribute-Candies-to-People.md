---
title: 1103.Distribute Candies to People
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 839276500
date: 2020-03-05 18:27:16
---
# 题目描述
We distribute some number of candies, to a row of n = num_people people in the following way:

We then give 1 candy to the first person, 2 candies to the second person, and so on until we give n candies to the last person.

Then, we go back to the start of the row, giving n + 1 candies to the first person, n + 2 candies to the second person, and so on until we give 2 * n candies to the last person.

This process repeats (with us giving one more candy each time, and moving to the start of the row after we reach the end) until we run out of candies.  The last person will receive all of our remaining candies (not necessarily one more than the previous gift).

Return an array (of length num_people and sum candies) that represents the final distribution of candies.

Example 1:
Input: candies = 7, num_people = 4
Output: [1,2,3,1]
Explanation:
On the first turn, ans[0] += 1, and the array is [1,0,0,0].
On the second turn, ans[1] += 2, and the array is [1,2,0,0].
On the third turn, ans[2] += 3, and the array is [1,2,3,0].
On the fourth turn, ans[3] += 1 (because there is only one candy left), and the final array is [1,2,3,1].

Example 2:
Input: candies = 10, num_people = 3
Output: [5,2,3]
Explanation: 
On the first turn, ans[0] += 1, and the array is [1,0,0].
On the second turn, ans[1] += 2, and the array is [1,2,0].
On the third turn, ans[2] += 3, and the array is [1,2,3].
On the fourth turn, ans[0] += 4, and the final array is [5,2,3]. 

Constraints:

1 <= candies <= 10^9
1 <= num_people <= 1000
# 我的解法
这道题目比较简单
```C++
class Solution {
public:
    vector<int> distributeCandies(int candies, int num_people) {
        vector<int> ans(num_people, 0);
        int candy = 1;
        while(candies > 0){
            for (int i = 0; i < num_people; i++){
                if (candy >= candies){
                    ans[i] += candies;
                    return ans;
                }
                ans[i] += candy;
                candies -= candy;
                candy++;
            }
        }
        return ans;
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Distribute Candies to People.
Memory Usage: 7.5 MB, less than 100.00% of C++ online submissions for Distribute Candies to People.

不过看了下题解，其实可以只用一个循环来完成
```C++

class Solution {
public:
    vector<int> distributeCandies(int candies, int num_people) {
        vector<int> ans(num_people, 0);
        int i = 0;
        while(candies != 0){
            ans[i % num_people] += min(candies, i + 1);
            candies -= min(candies, i + 1);
            i++;
        }
        return ans;
    }
};


```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Distribute Candies to People.
Memory Usage: 7.8 MB, less than 100.00% of C++ online submissions for Distribute Candies to People.
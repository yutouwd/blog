---
title: 13.Roman to Integer
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 866377430
date: 2020-02-24 15:32:36
---
# 题目描述
Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.

Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
For example, two is written as II in Roman numeral, just two one's added together. Twelve is written as, XII, which is simply X + II. The number twenty seven is written as XXVII, which is XX + V + II.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as IX. There are six instances where subtraction is used:

I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

Example 1:

Input: "III"
Output: 3
Example 2:

Input: "IV"
Output: 4
Example 3:

Input: "IX"
Output: 9
Example 4:

Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
Example 5:

Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.


# 我的解法

罗马数字转整数，通过一次从前往后遍历，来计算罗马数的大小。需要注意的是4和9以及40、90、400和900的情况。

```C++
class Solution {
public:
    int romanToInt(string s) {
        int ans = 0;
        for (int i = 0; i < s.size(); i++){
            switch (s[i]){
                case 'M':
                    ans += 1000;
                    break;
                case 'D':
                    ans += 500;
                    break;
                case 'C':
                    if (i + 1 < s.size() && s[i+1] == 'M'){
                        ans += 900;
                        i++;
                        break;
                    }
                    else if (i + 1 < s.size() && s[i+1] == 'D'){
                        ans += 400;
                        i++;
                        break;
                    }
                    else{
                        ans += 100;
                        break;
                    }
                case 'L':
                    ans += 50;
                    break;
                case 'X':
                    if (i + 1 < s.size() && s[i+1] == 'C'){
                        ans += 90;
                        i++;
                        break;
                    }
                    else if (i + 1 < s.size() && s[i+1] == 'L'){
                        ans += 40;
                        i++;
                        break;
                    }
                    else{
                        ans += 10;
                        break;
                    }
                case 'V':
                    ans += 5;
                    break;
                case 'I':
                    if (i + 1 < s.size() && s[i+1] == 'X'){
                        ans += 9;
                        i++;
                        break;
                    }
                    else if (i + 1 < s.size() && s[i+1] == 'V'){
                        ans += 4;
                        i++;
                        break;
                    }
                    else{
                        ans++;
                        break;
                    }
            }
        }
        return ans;
    }
};

```

Runtime: 4 ms, faster than 98.45% of C++ online submissions for Roman to Integer.
Memory Usage: 8.5 MB, less than 51.96% of C++ online submissions for Roman to Integer.

就是代码太长了，其实也可也从后往前遍历。如果后面的数字比当前位的数字要大，那么就是遇到了4和9的情况，这是就减去当前位的数字就可以了。
```C++
class Solution {
public:
    int romanToInt(string s) 
{
    unordered_map<char, int> T = { { 'I' , 1 },
                                   { 'V' , 5 },
                                   { 'X' , 10 },
                                   { 'L' , 50 },
                                   { 'C' , 100 },
                                   { 'D' , 500 },
                                   { 'M' , 1000 } };
                                   
   int sum = T[s.back()];
   for (int i = s.length() - 2; i >= 0; --i) 
   {
       if (T[s[i]] < T[s[i + 1]])
       {
           sum -= T[s[i]];
       }
       else
       {
           sum += T[s[i]];
       }
   }
   
   return sum;
}
};
```

Runtime: 12 ms, faster than 77.50% of C++ online submissions for Roman to Integer.
Memory Usage: 10.4 MB, less than 36.27% of C++ online submissions for Roman to Integer.


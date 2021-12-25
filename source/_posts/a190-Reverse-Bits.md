---
title: 190.Reverse Bits
tags:
  - leetcode
  - 位操作
categories:
  - leetcode
  - easy
copyright: true
comments: true
abbrlink: 328681550
date: 2020-03-02 18:59:14
---
# 题目描述
Reverse bits of a given 32 bits unsigned integer.

Example 1:
Input: 00000010100101000001111010011100
Output: 00111001011110000010100101000000
Explanation: The input binary string 00000010100101000001111010011100 represents the unsigned integer 43261596, so return 964176192 which its binary representation is 00111001011110000010100101000000.

Example 2:
Input: 11111111111111111111111111111101
Output: 10111111111111111111111111111111
Explanation: The input binary string 11111111111111111111111111111101 represents the unsigned integer 4294967293, so return 3221225471 which its binary representation is 10111111111111111111111111111111.
 

Note:

Note that in some languages such as Java, there is no unsigned integer type. In this case, both input and output will be given as signed integer type and should not affect your implementation, as the internal binary representation of the integer is the same whether it is signed or unsigned.
In Java, the compiler represents the signed integers using 2's complement notation. Therefore, in Example 2 above the input represents the signed integer -3 and the output represents the signed integer -1073741825.

# 我的解法
## 解题思路
依然是不太会做，参考<https://leetcode.com/problems/reverse-bits/discuss/54772/The-concise-C%2B%2B-solution(9ms)>
## 实现代码
```C++
class Solution {
public:
    uint32_t reverseBits(uint32_t n) {
        uint32_t ans;
        for (int i = 0; i < 32; i++)
            ans = (ans << 1) + (n >> i & 1);
        return ans;
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Reverse Bits.
Memory Usage: 7.1 MB, less than 100.00% of C++ online submissions for Reverse Bits.

思路大概是，循环32次，每次ans左移一位，加上n右移i位与1的结果。

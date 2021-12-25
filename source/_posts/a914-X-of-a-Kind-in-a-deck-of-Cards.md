---
title: 914.X of a Kind in a deck of Cards
tags:
  - leetcode
  - math
  - hashmap
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 4098248511
date: 2019-07-26 18:09:35
---
# 题目描述
In a deck of cards, each card has an integer written on it.

Return true if and only if you can choose X >= 2 such that it is possible to split the entire deck into 1 or more groups of cards, where:

Each group has exactly X cards.
All the cards in each group have the same integer.
 

Example 1:
Input: [1,2,3,4,4,3,2,1]
Output: true
Explanation: Possible partition [1,1],[2,2],[3,3],[4,4]

Example 2:
Input: [1,1,1,2,2,2,3,3]
Output: false
Explanation: No possible partition.

Example 3:
Input: [1]
Output: false
Explanation: No possible partition.

Example 4:
Input: [1,1]
Output: true
Explanation: Possible partition [1,1]

Example 5:
Input: [1,1,2,2,2,2]
Output: true
Explanation: Possible partition [1,1],[2,2],[2,2]

Note:

1 <= deck.length <= 10000
0 <= deck[i] < 10000
# 我的解法
## 解题思路
题目要求判断一个数组能否按要求分组，分组要求如下：
* 一个组里的数字的数值必须相等
* 每个组的size必须相等，并且大于等于2

我的想法是统计一下数组里面每一个数出现的频率统计一下，如果频率都能被一个数（大于等于2）整除就可以。所以用map来实现比较方便。

## 实现代码
```C++
class Solution {
public:
    bool hasGroupsSizeX(vector<int>& deck) {
        map<int,int> numOfcard;
        /*先将每个数字出现的次数统计一下*/
        for (int i = 0; i < deck.size(); i++){
            if (numOfcard.find(deck[i]) != numOfcard.end()){ //已经有数据
                numOfcard[deck[i]]++;
            }
            else{ //还没有添加数据
                numOfcard.insert({deck[i],1});
            }
        }
        if (numOfcard.size() == 1 && deck.size() != 1)
            return true;
        /*判断出现的数字的频率能不能被同一个数字整除*/
        int maxX = deck.size() / numOfcard.size() + 1;
        for (int i = 2; i < maxX; i++){
            int zeroMod = 0;
            for (auto iter = numOfcard.begin(); iter != numOfcard.end(); iter++){
                if (iter->second % i == 0)
                    zeroMod++;
            }
            if (zeroMod == numOfcard.size())
                return true;
        }
        return false;
    }
};
```
Runtime: 16 ms, faster than 80.38% of C++ online submissions for X of a Kind in a Deck of Cards.
Memory Usage: 9.8 MB, less than 52.47% of C++ online submissions for X of a Kind in a Deck of Cards.

提交了几次，用时不是特别稳定大概就16～24ms之间吧。
后来测试了一下，发现map里默认的value是0，所以就可以省略去第一个for里面的if和else判断了
```C++
class Solution {
public:
    bool hasGroupsSizeX(vector<int>& deck) {
        map<int,int> numOfcard;
        for (int i = 0; i < deck.size(); i++)
            numOfcard[deck[i]]++;
        if (numOfcard.size() == 1 && deck.size() != 1)
            return true;
        int maxX = deck.size() / numOfcard.size() + 1;
        for (int i = 2; i < maxX; i++){
            int zeroMod = 0;
            for (auto iter = numOfcard.begin(); iter != numOfcard.end(); iter++){
                if (iter->second % i == 0)
                    zeroMod++;
            }

            if (zeroMod == numOfcard.size())
                return true;
        }
        
        return false;
    }
};
```
# 高票解法
看了下高票的解法，发现居然能用5行就能实现的，太厉害了吧。
## 实现代码
```C++
    bool hasGroupsSizeX(vector<int>& deck) {
        unordered_map<int, int> count;
        int res = 0;
        for (int i : deck) count[i]++;
        for (auto i : count) res = __gcd(i.second, res);
        return res > 1;
    }
```
## 代码分析
首先就是for (int i : deck)这种用法就没怎么见过了，测试了一下
```C++
int main(int argc,char * argv[]){
    vector<int> testcase = {1,2,3,4,4,3,2,1};
    for (int i : testcase)
        cout << i << endl;
    return 0;
}
```
可以依次输出testcase里面的数字，感觉用法和iterator差不多只不过iterator返回的是地址，这个可以直接返回元素。好像是C++11的用法，参考：<https://en.cppreference.com/w/cpp/language/range-for>第一个for循环，就将deck数组里面数字出现的频率统计了一遍，并放到map里。

接下来第二个for循环遍历整个map，然后就一个求最大公约数的过程，__gcd就是可以求两个数的最大公约数，这个for循环就求了每个数字出现的频率的最大公约数。
# 知识总结
继续学习了map的用法，可以用两三句就可以把一个数组里出现的数据的频率统计了：
```C++
map<int, int> count;
for (int i : array)
    count[i]++;
```
还学了一种更简单的for循环的用法。
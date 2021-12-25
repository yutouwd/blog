---
title: 824.Goat Latin
tags:
  - leetcode
  - string
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 316802933
date: 2019-09-19 22:16:28
---
# 题目描述
A sentence S is given, composed of words separated by spaces. Each word consists of lowercase and uppercase letters only.

We would like to convert the sentence to "Goat Latin" (a made-up language similar to Pig Latin.)

The rules of Goat Latin are as follows:

If a word begins with a vowel (a, e, i, o, or u), append "ma" to the end of the word.
For example, the word 'apple' becomes 'applema'.
 
If a word begins with a consonant (i.e. not a vowel), remove the first letter and append it to the end, then add "ma".
For example, the word "goat" becomes "oatgma".
 
Add one letter 'a' to the end of each word per its word index in the sentence, starting with 1.
For example, the first word gets "a" added to the end, the second word gets "aa" added to the end and so on.
Return the final sentence representing the conversion from S to Goat Latin. 

Example 1:
Input: "I speak Goat Latin"
Output: "Imaa peaksmaaa oatGmaaaa atinLmaaaaa"

Example 2:
Input: "The quick brown fox jumped over the lazy dog"
Output: "heTmaa uickqmaaa rownbmaaaa oxfmaaaaa umpedjmaaaaaa overmaaaaaaa hetmaaaaaaaa azylmaaaaaaaaa ogdmaaaaaaaaaa"
 

Notes:

S contains only uppercase, lowercase and spaces. Exactly one space between each word.
1 <= S.length <= 150.

# 我的解法
## 解题思路
题目其实挺好理解的，就是要在每个单词的后面加上ma，如果单词是辅音开头的就要把辅音字母放到最后再加ma。之前做了一题是要把每个单词分开，一直没找到比较快的方法，这次还是看评论学会了一种方法。之后其实就很简单了。
## 实现代码
```C++
class Solution {
public:
    string toGoatLatin(string S) {
        unordered_set<char> vowel = {'a','e','i','o','u','A','E','I','O','U'};
        string ma = "maa";
        string tmp, re;
        istringstream ss(S);
        while(ss >> tmp){
            string ans;
            if (vowel.find(tmp[0]) != vowel.end()){
                ans = tmp;
                ans += ma;
            }
            else{
                ans = tmp.substr(1,tmp.size() - 1);
                ans += tmp[0];
                ans += ma;
            }
            re += ans;
            re += ' ';
            ma += 'a';
        }
        return re.substr(0,re.size() - 1);
    }
};
```

Runtime: 0 ms, faster than 100.00% of C++ online submissions for Goat Latin.
Memory Usage: 9.1 MB, less than 71.43% of C++ online submissions for Goat Latin.

# 知识总结
C++将string按空格分开可以用istringstream，在sstream头文件中。

set的用法，set和map的区别是set只有一个值，而map有key和value两个值。
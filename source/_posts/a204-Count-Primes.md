---
title: 204.Count Primes
tags:
  - leetcode
  - math
categories:
  - leetcode
  - easy
copyright: true
comments: true
notshow: true
abbrlink: 828591771
date: 2019-09-13 09:56:53
---
# 题目描述
Count the number of prime numbers less than a non-negative number, n.

Example:
Input: 10
Output: 4

Explanation: There are 4 prime numbers less than 10, they are 2, 3, 5, 7.

# 我的解法
## 解题思路
之前就做过了一题求质数的方法，记下了一种较为快速的求质数的方法。首先任何一个数都可以表示为一下形式：/{6n,6n+1,6n+2,6n+3,6n+4,6n+5/}(n=0,1,2...)，很显然6n,6n+2,6n+4能被2整除，6n+3能被3整除，所以只用考虑6n+1和6n+5的数。再加上一个数最大的因数小于等于它的开方，有了这几个条件就可以大大减少计算量了。

## 实现代码
```C++
class Solution {
public:
    bool isPrime(int n){
        if (n <= 3)
            return n > 1;
        if (n % 6 != 1 && n % 6 != 5)
            return false;
        int sqrt = std::sqrt(n);
        for (int i = 5; i <= sqrt; i+=6){
            if (n % i == 0 || n % (i+2) == 0)
                return false;
        }
        return true;
    }
    int countPrimes(int n) {
        int count = 0;
        for (int i = 1; i < n; i++){
            if (isPrime(i))
                count++;
        }
        return count;
    }
};
```

Runtime: 168 ms, faster than 24.06% of C++ online submissions for Count Primes.
Memory Usage: 8.2 MB, less than 95.83% of C++ online submissions for Count Primes.

但是速度还是有点点的慢呀

# 高票解法
厄拉多筛选法：声明一个长度为n的数组。从2开始，将2的倍数都标记出来；然后将3的倍数也都标记出来；因为4已经是2的倍数了，所以是4的倍数也应定是2的倍数，就不考虑4的倍数。然后在把5的倍数标记出来...
## 实现代码
```C++
class Solution {
public:
    int countPrimes(int n) {
        vector<bool> isPrime(n, true);
        int count = 0;
        for (int i = 2; i < n; i++){
            if (isPrime[i]){
                count++;
                for (int j = i+i; j < n; j += i){
                    isPrime[j] = false;
                }
            }
        }
        return count;
    }
};
```

Runtime: 80 ms, faster than 42.73% of C++ online submissions for Count Primes.
Memory Usage: 8.7 MB, less than 54.17% of C++ online submissions for Count Primes.

时间快了很多，但是看其他更快的也基本都是用这种方法的，不知道是不是测试用例更新了。

## 继续优化
又看到了一个更快的方法，使用了一些tricks
```C++
class Solution {
public:
    int countPrimes(int n) {
        if (n <= 2) return 0;
        if (n == 3) return 1;
        vector<bool> isPrime(n, true);
        int count = n - 2;
        int rt = sqrt(n); // 只用计算到sqrt(n)
        for (int i = 2; i <= rt; i++){
            if (isPrime[i]){
                for (int j = i*i; j < n; j += i){  // 从i*i开始而不是i+i，因为比如说6，已经被2筛选过了
                    if (isPrime[j]){
                        isPrime[j] = false;
                        count--;
                    }
                }
            }
        }
        
        return count;
    }
};
```
Runtime: 64 ms, faster than 59.63% of C++ online submissions for Count Primes.
Memory Usage: 8.8 MB, less than 45.83% of C++ online submissions for Count Primes.

# 知识总结
学习了求质数较为快速的方法
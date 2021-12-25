---
title: 53.Maximum Subarray
tags:
  - leetcode
  - math
  - 分治法
  - 动态规划
categories:
  - leetcode
  - Easy
copyright: true
comments: true
notshow: true
abbrlink: 1411250823
date: 2019-09-11 22:38:19
---
# 题目描述
Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

Example:
Input: [-2,1,-3,4,-1,2,1,-5,4],
Output: 6
Explanation: [4,-1,2,1] has the largest sum = 6.

Follow up:
If you have figured out the O(n) solution, try coding another solution using the divide and conquer approach, which is more subtle.
# 我的解法
## 解题思路

今天笔试的时候遇到的一个题目，就想到了用暴力的做法，就是遍历数组两遍，把所有的可能都算出来
## 实现代码

```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int maxSum = INT_MIN;
        int curSum = 0;
        for (int i = 0; i < nums.size(); i++){
            curSum = nums[i];
            if (curSum > maxSum)
                maxSum = curSum;
            for (int j = i + 1; j < nums.size(); j++){
                curSum += nums[j];
                if (curSum > maxSum){
                    maxSum = curSum;
                }
            }
        }
        return maxSum;
    }
};
```
Runtime: 308 ms, faster than 5.00% of C++ online submissions for Maximum Subarray.
Memory Usage: 9.2 MB, less than 99.02% of C++ online submissions for Maximum Subarray.

速度真的好慢。。。因为时间复杂度是O(n^2)吧

# 一次遍历
看到一个[python实现][1]的一次遍历的方法，转成了C++代码。不得不说C++都没有大于两个max的函数，还要自己写一个，比python麻烦多了。不过后来发现其实这个程序里不需要用到四个参数的max，自己也把程序简化了一下，去除了一些多余的判断。

思路就是使用两个变量，一个记录当前子集的和，另一个记录最大子集的和。然后在遍历的过程中判断如果当前的子集（不包括当前值）是不是大于0：如果大于零就把当前值加到当前子集的和中，然后判断是当前子集大还是最大子集大，并更新最大子集；如果是小于等于零就可以认为这个子集对于构成一个最大和的子集是没有贡献的，然后就从当前值开始构成当前子集，并继续开始判断。

```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if (nums.size() == 1) return nums[0];
        //使用两个变量，一个记录最大的和，一个记录当前的和
        int curSum = nums[0]; // 当前子集的和
        int maxSum = curSum;    // 最大的和
        for (int i = 1; i < nums.size(); i++){
            // 如果当前子集为正值，就把当前值加到当前子集中，再判断是之前的最大子集大还是当前子集大
            if (curSum > 0){
                curSum += nums[i];
                maxSum = max(maxSum, curSum + nums[i]);
            }
            // 如果当前子集为0或者负数那么从当前值开始往后求后面的子集
            else{
                maxSum = max(maxSum, nums[i]);
                curSum = nums[i];
            }
        }
        return max_;
    }
};
```

Runtime: 4 ms, faster than 98.58% of C++ online submissions for Maximum Subarray.
Memory Usage: 9.1 MB, less than 100.00% of C++ online submissions for Maximum Subarray.

只用4ms了，快了真的不是一点半点，算法时间复杂度O(n)，空间复杂度O(1)。

# 分治法

分治法其实一开始没有看懂，直到自己用手把测试用例推了一遍才大概明白。思路还是将一个问题分解成更小的问题，只不过这里要分解成3个问题，因为如果直接将数组分成两个数组会遇到最大子集在两个数组中间的情况，所以要取一个middle=(start+end)/2，分解成\[start,middle-1\]，\[middle+1,end\]，然后还要考虑middle的问题，就要将middle往两遍遍历，求出向左和向右的最大子集，方法和一次遍历的类似。最后比较左边数组、右边数组和middle加上向左和向右的最大子集（小于零就加零）的最大值。

这样看来这道题目使用分治法比其他方法要麻烦挺多的，时间复杂度也是O(nlogn)，思路也相对更难理解，主要是因为不能直接分解成两个问题吧。

```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        return find(nums, 0, nums.size() - 1);
    }
    int find(vector<int>& nums, int start, int end){
        // 边界条件
        if (start == end) return nums[start];
        if (start > end) return INT_MIN;
        
        int left_max = 0, right_max = 0, ml = 0, mr = 0;
        int middle = (start + end) / 2;
        
        left_max = find(nums, start, middle - 1);
        right_max = find(nums, middle + 1, end);
        
        // middle to left
        for (int i = middle - 1, sum = 0; i >= start; i--){
            sum += nums[i];
            if (ml < sum) ml = sum;
        }
        // middle to right
        for (int i = middle + 1, sum = 0; i <= end; i++){
            sum += nums[i];
            if (mr < sum) mr = sum;
        }
        
        return max(max(left_max, right_max), ml + mr + nums[middle]);
    }
};
```

# 动态规划
看了一个视频感觉豁然开朗，<https://www.bilibili.com/video/av38722679>
要用动态规划要具备两个性质，重叠子问题和最优子问题
* 最优子问题：如果一个问题的最优解包含了其中子问题的最优解，那么称其有最优子结构
* 重叠子问题：当解决一个问题时，往往依赖其更小规模的子问题的解，甚至依赖与若干个规模更小的子问题的解。

对于这道题目来说：
* 最优子问题：很明显对于最大的子集最优子问题是符合的
* 重叠子问题：对于当前的解，需要用到之前子集求出来的解（感觉有点解释不清楚）

状态转移方程为： dp[i] = max(nums[i], nums[i] + dp[i])

以\[-2,1,-3,4,-1,2,1,-5,4\]为例子
1. \[-2\]的最大子集显然就是它自己本身，所以dp=\[-2\]
2. \[-2,1\]的子集有{-2,-1,1}，最大子集就是1了，dp=\[-2,1\]
3. 对于\[-2,1,-3\]，上一个子集的解是1，加上-3为-2，dp=\[-2,1,-2\]
...

```C++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        if (nums.size() == 0) return 0;
        vector<int> dp(nums.size(), 0); 
        dp[0] = nums[0]; 
        int max = dp[0];
        for (int i = 1; i < nums.size(); i++){
            dp[i] = nums[i] > nums[i] + dp[i - 1] ? nums[i] : nums[i] + dp[i - 1];
            if (dp[i] > max) max = dp[i];
        }
        return max;
    }
};
```
Runtime: 4 ms, faster than 98.60% of C++ online submissions for Maximum Subarray.
Memory Usage: 9.5 MB, less than 9.80% of C++ online submissions for Maximum Subarray.

感觉思路其实和一次遍历是差不多的，不同的是需要一个同样大小的数组来记录之前的解。


[1]:https://leetcode-cn.com/problems/maximum-subarray/solution/bao-li-qiu-jie-by-pandawakaka/
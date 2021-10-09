# AcWing 算法基础课 -- 基础算法

## AcWing 795. 前缀和 

`难度：简单`

### 题目描述

输入一个长度为n的整数序列。

接下来再输入m个询问，每个询问输入一对l, r。

对于每个询问，输出原序列中从第l个数到第r个数的和。

**输入格式**

第一行包含两个整数n和m。

第二行包含n个整数，表示整数数列。

接下来m行，每行包含两个整数l和r，表示一个询问的区间范围。

**输出格式**

共m行，每行输出一个询问的结果。

```r
数据范围

1≤l≤r≤n,
1≤n,m≤100000,
−1000≤数列中元素的值≤1000

输入样例：

5 3
2 1 3 6 4
1 2
1 3
2 4

输出样例：

3
6
10
```

### Solution

```java
class NumArray {
public:
    vector<int> mysum;
    NumArray(vector<int>& nums) {
        int n = nums.size();
        mysum.resize(n+1);
        for(int i=1;i<=n;i++)
            mysum[i] = mysum[i-1]+nums[i-1];
    }
    
    int sumRange(int left, int right) {
        left++;
        right++;
        return mysum[right]-mysum[left-1];
    }
};
```

[303. 区域和检索 - 数组不可变](https://leetcode-cn.com/problems/range-sum-query-immutable/)


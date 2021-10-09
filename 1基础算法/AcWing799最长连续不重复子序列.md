# AcWing 算法基础课 -- 基础算法

## AcWing 799. 最长连续不重复子序列

`难度：简单`

### 题目描述

给定一个长度为n的整数序列，请找出最长的不包含重复的数的连续区间，输出它的长度。

**输入格式**

第一行包含整数n。

第二行包含n个整数（均在0~100000范围内），表示整数序列。

**输出格式**

共一行，包含一个整数，表示最长的不包含重复的数的连续区间的长度。

```r
数据范围

1≤n≤100000

输入样例：

5
1 2 2 3 5

输出样例：

3
```

### Solution

```c++
#include<bits/stdc++.h>
using namespace std;

const int maxn = 1e6+6;
int a[maxn];
int n;

int main(){
    cin>>n;
    for(int i=0;i<n;i++)
        cin>>a[i];

    int l=0;
    int r=0;
    unordered_map<int, int> mmap;
    int ans = 0;

    while(r<n){
        int c = a[r];
        r++;
        mmap[c]++;
        while(mmap[c]>1){
            int d = a[l];
            l++;
            mmap[d]--;
        }
        ans = max(ans,r-l);
    }
    cout<<ans;
    return 0;
}
```


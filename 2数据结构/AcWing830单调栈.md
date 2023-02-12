# AcWing 算法基础课 -- 数据结构

## AcWing 830. 单调栈 

`难度：简单`

### 题目描述

给定一个长度为N的整数数列，输出每个数左边第一个比它小的数，如果不存在则输出-1。

**输入格式**

第一行包含整数N，表示数列长度。

第二行包含N个整数，表示整数数列。

**输出格式**

共一行，包含N个整数，其中第i个数表示第i个数的左边第一个比它小的数，如果不存在则输出-1。

```r
数据范围

1≤N≤105

1≤数列中元素≤109

输入样例：

5
3 4 2 7 5

输出样例：

-1 3 -1 2 2
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;
int a[N];
int ans[N];
stack<int> st;

int main() {
    int n;
    cin >> n;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    for (int i = 0; i < n; i++) {
        while (!st.empty() && a[i] <= st.top()) {
            st.pop();
        }
        ans[i] = (!st.empty()?st.top():-1);
        st.push(a[i]);
    }
    for(int i=0;i<n;i++){
        cout<<ans[i]<<" ";
    }
    return 0;
}
```
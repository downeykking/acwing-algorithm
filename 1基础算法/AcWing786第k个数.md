# AcWing 算法基础课 -- 基础算法

## AcWing 786. 第k个数 

`难度：简单`

### 题目描述

给定一个长度为n的整数数列，以及一个整数k，请用快速选择算法求出数列从小到大排序后的第k个数。

**输入格式**

输入共两行，第一行包含两个整数 n 和 k。

第二行包含 n 个整数（所有整数均在$1~10^9$范围内），表示整个数列。

**输出格式**

输出一个整数，表示数列的第k小数。

**数据范围**

1 ≤ n ≤ 100000
1 ≤ k ≤ n

**输入样例**：

```
5 3
2 4 1 5 3
```

**输出样例**：

```
3
```

### Solution

```java 
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5+5;
int a[maxn];

int partition(int arr[], int l, int r){
    int pivot = arr[l];
    int i=l;
    int j=r;
    while(i<j){
        while(i<j&&arr[j]>=pivot)
            j--;
        while(i<j&&arr[i]<=pivot)
            i++;
        if(i<j)
            swap(arr[i],arr[j]);
    }
    swap(arr[i],arr[l]);
    return i;
}

int qsort(int arr[], int l, int r, int k){
    if(l<r){
        int index = partition(arr,l,r);
        if(index==k)
            return index;
        else if(index<k)
            return qsort(arr,index+1,r,k);
        else
            return qsort(arr,l,index-1,k);
    }
}

int main(){
    int n;
    int k;
    cin>>n>>k;
    for(int i=0;i<n;i++)
        cin>>a[i];
    int ans = qsort(a,0,n-1,k-1);
    cout<<a[ans];
    return 0;
}
```


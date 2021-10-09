# AcWing 算法基础课 -- 基础算法

## AcWing 787. 归并排序

`难度：简单`

### 题目描述

给定你一个长度为n的整数数列。

请你使用快速排序对这个数列按照从小到大进行排序。

并将排好序的数列按顺序输出。

**输入格式**

输入共两行，第一行包含整数 n。

第二行包含 n 个整数（所有整数均在$1~10^9$范围内），表示整个数列。

**输出格式**

输出共一行，包含 n 个整数，表示排好序的数列。

**数据范围**

1 ≤ n ≤ 100000

**输入样例**：

```
5
3 1 2 4 5
```

**输出样例**：

```
1 2 3 4 5
```

### Solution

```java
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5+5;
int a[maxn];
int temp[maxn];

void mergesort(int arr[], int l, int r){
    if(l>=r) return;
    int mid = l+r>>1;
    mergesort(arr,l,mid);
    mergesort(arr,mid+1,r);
    int k=0;
    int i=l;
    int j=mid+1;
    while(i<=mid&&j<=r){
        if(arr[i]<=arr[j])
            temp[k++] = arr[i++];
        else
            temp[k++] = arr[j++];
    }
    while(i<=mid)
        temp[k++] = arr[i++];
    while(j<=r)
        temp[k++] = arr[j++];
    for (int i=l,j=0;i<=r;i++,j++){
		arr[i] = temp[j];
	}
}

int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++)
        cin>>a[i];
    mergesort(a,0,n-1);
    for(int i=0;i<n;i++)
        cout<<a[i]<<" ";
    return 0;
}
```


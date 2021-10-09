# AcWing 算法基础课 -- 基础算法

## AcWing 785. 快速排序 

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

### Solution1

```java 
//常规模板 可能退化到O(n2) 卡某个样例
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5+5;
int a[maxn];

int partition(int arr[], int l, int r){
    int pivot = arr[l];
    int i=l;
    int j=r;
    while(i<j){
        //先j再i
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

void qsort(int arr[], int l, int r){
    if(l>=r) return;
    int index = partition(arr,l,r);
    qsort(arr,l,index-1);
    qsort(arr,index+1,r);
}

int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++)
        cin>>a[i];
    qsort(a,0,n-1);
    for(int i=0;i<n;i++)
        cout<<a[i]<<" ";
    return 0;
}
```

#### Solution2

```
//标准模板
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5+5;
int a[maxn];

void qsort(int arr[], int l, int r){
    if(l>=r) return;
    int i=l-1;
    int j=r+1;
    int pivot = arr[i+j>>1];
    while(i<j){
        do i++; while(arr[i]<pivot);
        do j--; while(arr[j]>pivot);
        if(i<j)
            swap(arr[i],arr[j]);
    }
    qsort(arr,l,j);
    qsort(arr,j+1,r);
}

int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++)
        cin>>a[i];
    qsort(a,0,n-1);
    for(int i=0;i<n;i++)
        cout<<a[i]<<" ";
    return 0;
}
```

[acwing785](https://www.acwing.com/solution/content/23415/)


# AcWing 算法基础课 -- 基础算法

## AcWing 789. 数的范围 

`难度：简单`

### 题目描述

给定一个按照升序排列的长度为n的整数数组，以及 q 个查询。

对于每个查询，返回一个元素k的起始位置和终止位置（位置从0开始计数）。

如果数组中不存在该元素，则返回“-1 -1”。
输入格式

第一行包含整数n和q，表示数组长度和询问个数。

第二行包含n个整数（均在1~10000范围内），表示完整数组。

接下来q行，每行包含一个整数k，表示一个询问元素。
输出格式

共q行，每行包含两个整数，表示所求元素的起始位置和终止位置。

如果数组中不存在该元素，则返回“-1 -1”。

**数据范围**
```r
1≤n≤100000
1≤q≤10000
1≤k≤10000
```
**输入样例**：
```r
6 3
1 2 2 3 3 4
3
4
5
```
**输出样例**：
```r
3 4
5 5
-1 -1
```

### Solution

```java
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5+5;
int n, q, x, a[maxn];

int main() {
    scanf("%d%d", &n, &q);
    for (int i = 0; i < n; i++)    
        scanf("%d", &a[i]);
    while (q--) {
        scanf("%d", &x);
        int l = 0, r = n-1;
        while(l<r){
            int mid = l + (r - l >> 1);
            if(a[mid]>=x)
                r = mid;
            else
                l = mid+1;
        }
        
        int ans1 = (a[l]==x?l:-1);

        l = 0, r = n-1;
        while(l<r){
            int mid = l + (r - l >> 1);
            if(a[mid]<=x)
                l = mid;
            else
                r = mid-1;
        }
        int ans2 = (a[l]==x?l:-1);
        printf("%d %d\n",ans1,ans2);
    } 
    
    return 0;
}
```


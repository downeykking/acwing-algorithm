# AcWing 算法基础课 -- 基础算法

## AcWing 797. 差分 

`难度：简单`

### 题目描述

输入一个长度为n的整数序列。

接下来输入m个操作，每个操作包含三个整数l, r, c，表示将序列中[l, r]之间的每个数加上c。

请你输出进行完所有操作后的序列。

**输入格式**

第一行包含两个整数n和m。

第二行包含n个整数，表示整数序列。

接下来m行，每行包含三个整数l，r，c，表示一个操作。

**输出格式**

共一行，包含n个整数，表示最终序列。


```r
数据范围

1≤n,m≤100000,
1≤l≤r≤n,
−1000≤c≤1000,
−1000≤整数序列中元素的值≤1000

输入样例：

6 3
1 2 2 1 2 1
1 3 1
3 5 1
1 6 1

输出样例：

3 4 5 3 4 2
```

### Solution

```java
//差分 时间复杂度 o(m)
//原数组a[]，差分数组b[]，都从1开始
//差分数组的前缀和是原数组
#include<iostream>
using namespace std;
const int N=1e5+10;
int a[N],b[N]; 
int main(){
    int n,m;
    scanf("%d%d",&n,&m);
    for(int i=1;i<=n;i++) {
        scanf("%d",&a[i]);
        b[i]=a[i]-a[i-1];      //构建差分数组
    }
    int l,r,c;
    
    while(m--){
        scanf("%d%d%d",&l,&r,&c);
        b[l]+=c;     //表示将序列中[l, r]之间的每个数加上c
        b[r+1]-=c;
    }
    
    for(int i=1;i<=n;i++) 
{
        b[i]+=b[i-1];  //求前缀和运算
        printf("%d ",b[i]);
    }
    return 0;
}
```

[CSDN](https://blog.csdn.net/weixin_45629285/article/details/111146240)
# AcWing 算法基础课 -- 数据结构

## AcWing 154. 滑动窗口 

`难度：简单`

### 题目描述

给定一个大小为 $n≤10^6$

的数组。

有一个大小为k的滑动窗口，它从数组的最左边移动到最右边。

您只能在窗口中看到k个数字。

每次滑动窗口向右移动一个位置。

以下是一个例子：

该数组为[1 3 -1 -3 5 3 6 7]，k为3。

```r
窗口位置 	最小值 	最大值
[1 3 -1] -3 5 3 6 7 	-1 	3
1 [3 -1 -3] 5 3 6 7 	-3 	3
1 3 [-1 -3 5] 3 6 7 	-3 	5
1 3 -1 [-3 5 3] 6 7 	-3 	5
1 3 -1 -3 [5 3 6] 7 	3 	6
1 3 -1 -3 5 [3 6 7] 	3 	7
```

您的任务是确定滑动窗口位于每个位置时，窗口中的最大值和最小值。

**输入格式**

输入包含两行。

第一行包含两个整数n和k，分别代表数组长度和滑动窗口的长度。

第二行有n个整数，代表数组的具体数值。

同行数据之间用空格隔开。

**输出格式**

输出包含两个。

第一行输出，从左至右，每个位置滑动窗口中的最小值。

第二行输出，从左至右，每个位置滑动窗口中的最大值。

```r
输入样例：

8 3
1 3 -1 -3 5 3 6 7

输出样例：

-1 -3 -3 -3 3 3
3 3 5 5 6 7
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;
int a[N];
int ansmax[N], ansmin[N];
deque<int> qmax, qmin;

int main() {
    memset(ansmax, -1, sizeof(ansmax));
    memset(ansmin, -1, sizeof(ansmin));
    int n, k;
    cin >> n >> k;
    for (int i = 0; i < n; i++) {
        cin >> a[i];
    }
    for (int i = 0; i < n; i++) {
        // 在窗口外 毕业了
        if(!qmax.empty()&&i-qmax.front()>=k){
            qmax.pop_front();
        }
        // 队首最大 单调减
        while(!qmax.empty()&&a[i]>a[qmax.back()])
            qmax.pop_back();
        qmax.push_back(i);
        if(i>=k-1){
            ansmax[i] = a[qmax.front()];
        }
    }

    for (int i = 0; i < n; i++) {
        // 在窗口外 毕业了
        if(!qmin.empty()&&i-qmin.front()>=k){
            qmin.pop_front();
        }
        // 队首最小 单调增
        while(!qmin.empty()&&a[i]<a[qmin.back()])
            qmin.pop_back();
        qmin.push_back(i);
        if(i>=k-1){
            ansmin[i] = a[qmin.front()];
        }
    }
    for(int i=k-1;i<n;i++){
        cout<<ansmin[i]<<" ";
    }
    cout<<endl;
    for(int i=k-1;i<n;i++){
        cout<<ansmax[i]<<" ";
    }
    return 0;
}
```
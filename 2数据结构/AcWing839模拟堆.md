# AcWing 算法基础课 -- 数据结构

## AcWing 839. 模拟堆

`难度：简单`

### 题目描述

维护一个集合，初始时集合为空，支持如下几种操作：
“I x”，插入一个数x；
“PM”，输出当前集合中的最小值；
“DM”，删除当前集合中的最小值（数据保证此时的最小值唯一）；
“D k”，删除第k个插入的数；
“C k x”，修改第k个插入的数，将其变为x；
现在要进行N次操作，对于所有第2个操作，输出当前集合的最小值。

**输入格式**

第一行包含整数N。

接下来N行，每行包含一个操作指令，操作指令为”I x”，”PM”，”DM”，”D k”或”C k x”中的一种。

**输出格式**

对于每个输出指令“PM”，输出一个结果，表示当前集合中的最小值。

每个结果占一行。

**数据范围**

$1≤N≤105$

$−109≤x≤109$

数据保证合法。



```
输入样例：
8
I -10
PM
I -10
D 1
C 2 8
I 6
PM
DM

输出样例：
-10
6
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 100010;
int h[N], hp[N], ph[N], sz;
// ph[k]存储第 k 个插入的点在堆中的位置
// hp[m]存储堆中下标是 m 的点是第几个插入的
// root=1
// 小根堆
void heap_swap(int a, int b) {
    std::swap(ph[hp[a]], ph[hp[b]]);
    std::swap(hp[a], hp[b]);
    std::swap(h[a], h[b]);
}

void up(int x) {
    while (x > 1 && h[x] < h[x / 2]) {
        heap_swap(x, x / 2);
        x /= 2;
    }
}

void down(int x) {
    while (x * 2 <= sz) {
        int t = 2 * x;
        // 把大的换上来
        if (t + 1 <= sz && h[t + 1] < h[t]) {
            t++;
        }
        if (h[x] >= h[t])
            break;
        heap_swap(x, t);
        x = t;
    }
    // 递归版本
    // int t = x;
    // if (2 * x <= sz && h[t] > h[2 * x])
    //     t = 2 * x;
    // if (2 * x + 1 <= sz && h[t] > h[2 * x + 1])
    //     t = 2 * x + 1;
    // if (t != x) {
    //     heap_swap(t, x);
    //     down(t);
    // }
}

int main() {
    int n;
    cin >> n;
    int m = 0;
    while (n--) {
        string op;
        int k, x;
        cin >> op;
        if (op == "I") {
            cin >> x;
            m++;
            h[++sz] = x;
            hp[sz] = m;
            ph[m] = sz;
            up(sz);
        }
        else if (op == "PM")
            cout << h[1] << endl;
        else if (op == "DM") {
            heap_swap(1, sz);
            sz--;
            down(1);
        }
        else if (op == "D") {
            cin >> k;
            int u = ph[k];
            heap_swap(u, sz);
            sz--;
            down(u);
            up(u);
        }
        else if (op == "C") {
            cin >> k >> x;
            h[ph[k]] = x;
            down(ph[k]);
            up(ph[k]);
        }
    }
    return 0;
}

```


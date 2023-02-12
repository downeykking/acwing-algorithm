# AcWing 算法基础课 -- 数据结构

## AcWing 837. 连通块中点的数量 

`难度：简单`

### 题目描述

给定一个包含n个点（编号为1~n）的无向图，初始时图中没有边。

现在要进行m个操作，操作共有三种：

- “C a b”，在点a和点b之间连一条边，a和b可能相等；
- “Q1 a b”，询问点a和点b是否在同一个连通块中，a和b可能相等；
- “Q2 a”，询问点a所在连通块中点的数量；

**输入格式**

第一行输入整数n和m。

接下来m行，每行包含一个操作指令，指令为“C a b”，“Q1 a b”或“Q2 a”中的一种。

**输出格式**

对于每个询问指令”Q1 a b”，如果a和b在同一个连通块中，则输出“Yes”，否则输出“No”。

对于每个询问指令“Q2 a”，输出一个整数表示点a所在连通块中点的数量

每个结果占一行。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

5 5
C 1 2
Q1 1 2
Q2 1
C 2 5
Q2 5

输出样例：

Yes
2
3
```

### Solution

这道题在并查集的基础上，还有一个计算每个连通块的点的数量。

每个连通块的点的数量也就是这个连通块根节点所在连通块中点的数量。
```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 100010;
int fa[N], cnt[N];

void init(int n) {
    for (int i = 1; i <= n; i++) {
        cnt[i] = 1;
        fa[i] = i;
    }
}

int find(int x) { return fa[x] == x ? x : (fa[x] = find(fa[x])); }

int main() {
    int n, m;
    cin >> n >> m;
    init(n);
    string op;
    int a, b;
    for (int i = 0; i < m; i++) {
        string op;
        cin >> op;
        if (op == "C") {
            cin >> a >> b;
            if (find(a) != find(b)) {
                fa[find(a)] = find(b);
                cnt[b] = cnt[b] + cnt[a];
            }
        }
        if (op == "Q1") {
            cin >> a >> b;
            if (find(a) == find(b))
                cout << "Yes" << endl;
            else
                cout << "No" << endl;
        }
        if (op == "Q2") {
            cin >> a;
            cout << cnt[fa[a]];
        }
    }
    return 0;
}
```
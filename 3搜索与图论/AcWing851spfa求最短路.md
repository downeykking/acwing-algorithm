# AcWing 算法基础课 -- 搜索与图论

## AcWing 851. spfa求最短路

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环， 边权可能为负数。

请你求出1号点到n号点的最短距离，如果无法从1号点走到n号点，则输出impossible。

数据保证不存在负权回路。

**输入格式**

第一行包含整数n和m。

接下来m行每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

**输出格式**

输出一个整数，表示1号点到n号点的最短距离。

如果路径不存在，则输出”impossible”。

**数据范围**

$1≤n,m≤10^5,$

图中涉及边长绝对值均不超过10000。

```r
输入样例：

3 3
1 2 5
2 3 -3
1 3 4

输出样例：

2
```

### Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5 + 5;
const int inf = 0x3f3f3f3f;
struct edge {
    int u, v, w;
    edge(int u, int v, int w) : u(u), v(v), w(w){};
};

vector<edge> g[maxn];
int d[maxn];
int inqueue[maxn];
queue<int> q;

void addedge(int u, int v, int w) { g[u].push_back(edge(u, v, w)); }

void init() { memset(d, 0x3f, sizeof(d)); }

void spfa(int s) {
    d[s] = 0;
    q.push(s);
    inqueue[s] = 1;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        inqueue[u] = 0;
        for (int i = 0; i < g[u].size(); i++) {
            edge e = g[u][i];
            if (d[e.v] > d[u] + e.w) {
                d[e.v] = d[u] + e.w;
                if (!inqueue[e.v]) {
                    q.push(e.v);
                    inqueue[e.v] = 1;
                }
            }
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m;
    int u, v, w;
    init();
    for (int i = 0; i < m; i++) {
        cin >> u >> v >> w;
        addedge(u, v, w);
    }
    spfa(1);
    if (d[n] != inf)
        cout << d[n];
    else
        cout << "impossible";
    return 0;
}
```
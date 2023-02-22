# AcWing 算法基础课 -- 搜索与图论

## AcWing 849. Dijkstra求最短路 II  

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环，所有边权均为非负值。

请你求出1号点到n号点的最短距离，如果无法从1号点走到n号点，则输出-1。

**输入格式**

第一行包含整数n和m。

接下来m行每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

**输出格式**

输出一个整数，表示1号点到n号点的最短距离。

如果路径不存在，则输出-1。

**数据范围**

$1≤n,m≤1.5\times10^5,$

图中涉及边长均不小于0，且不超过10000。

数据保证：如果最短路存在，则最短路的长度不超过$10^9$

```r
输入样例：

3 3
1 2 2
2 3 1
1 3 4

输出样例：

3
```

### Solution

因为节点数很少，朴素dij用邻接矩阵存

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1.5e5 + 5;
const int inf = 0x3f3f3f3f;

int d[maxn];
int vis[maxn];

struct edge {
    int u, v, w;
    edge(int u, int v, int w) : u(u), v(v), w(w){};
};

vector<edge> g[maxn];
typedef pair<int, int> pii;

int n, m;

void init() { memset(d, 0x3f, sizeof(d)); }

void addedge(int u, int v, int w) { g[u].push_back(edge(u, v, w)); }

int dijkstra(int s) {
    d[s] = 0;
    priority_queue<pii, vector<pii>, greater<pii>> pq;
    pq.push({0, s});

    while (!pq.empty()) {
        pii now = pq.top();
        pq.pop();
        // 如果已经处理过了,是一个冗余的备份(比如重边)
        if (vis[now.second])
            continue;
        vis[now.second] = 1;
        for (int i = 0; i < g[now.second].size(); i++) {
            edge e = g[now.second][i];
            if (d[e.v] > d[e.u] + e.w) {
                d[e.v] = d[e.u] + e.w;
                pq.push({d[e.v], e.v});
            }
        }
    }
    if (d[n] == inf)
        return -1;
    return d[n];
}
int main() {
    cin >> n >> m;
    int u, v, w;
    init();
    for (int i = 0; i < m; i++) {
        cin >> u >> v >> w;
        addedge(u, v, w);
    }
    cout << dijkstra(1);
    return 0;
}

```
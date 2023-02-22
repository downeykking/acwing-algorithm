# AcWing 算法基础课 -- 搜索与图论

## AcWing 849. Dijkstra求最短路 I  

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环，所有边权均为正值。

请你求出1号点到n号点的最短距离，如果无法从1号点走到n号点，则输出-1。

**输入格式**

第一行包含整数n和m。

接下来m行每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

**输出格式**

输出一个整数，表示1号点到n号点的最短距离。

如果路径不存在，则输出-1。

**数据范围**

$1≤n≤500,$
$1≤m≤10^5,$

图中涉及边长均不超过10000。

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

```java
#include <bits/stdc++.h>
using namespace std;

const int maxn = 500 + 5;

int d[maxn];
int g[maxn][maxn];
int vis[maxn];

void init() { memset(d, 0x3f, sizeof(d)); }

int dijkstra(int n) {
    d[1] = 0;
    for (int i = 1; i <= n; i++) {
        int t = -1;
        for (int j = 1; j <= n; j++) {
            if (!vis[j] && (t == -1 || d[j] < d[t])) {
                t = j;
            }
        }
        vis[t] = 1;
        for (int j = 1; j <= n; j++) {
            d[j] = min(d[j], d[t] + g[t][j]);
        }
    }
    if (d[n] == 0x3f3f3f3f)
        return -1;
    return d[n];
}

int main() {
    int n, m;
    cin >> n >> m;
    int u, v, w;
    init();
    for (int i = 0; i < m; i++) {
        cin >> u >> v >> w;
        if(g[u][v])
            g[u][v] = min(w, g[u][v]);
        else
            g[u][v] = w;
    }
    cout << dijkstra(n);
    return 0;
}
```
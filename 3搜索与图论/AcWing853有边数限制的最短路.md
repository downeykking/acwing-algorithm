# AcWing 算法基础课 -- 搜索与图论

## AcWing 853. 有边数限制的最短路

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环， 边权可能为负数。

请你求出从1号点到n号点的最多经过k条边的最短距离，如果无法从1号点走到n号点，输出impossible。

注意：图中可能 存在负权回路 。

**输入格式**

第一行包含三个整数n，m，k。

接下来m行，每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

**输出格式**

输出一个整数，表示从1号点到n号点的最多经过k条边的最短距离。

如果不存在满足条件的路径，则输出“impossible”。

**数据范围**

$1≤n,k≤500,$
$1≤m≤10000,$

任意边长的绝对值不超过10000。

```r
输入样例：

3 3 1
1 2 1
2 3 1
1 3 3

输出样例：

3
```

### Solution

Bellman-Ford算法

时间复杂度 $O(nm)$, n 表示点数，m 表示边数

**一般 spfa 性能比 Bellman-Ford 好，只有特殊情况下用 Bellman-Ford 算法，比如这题有边的数量的限制**

1. 思路
```r
for n 次
    for 所有边 a,b,w
        dist[b] = min(dist[b], dist[a] + w)
```

2. 解题代码

```java
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5 + 5;
const int inf = 0x3f3f3f3f;
struct edge {
    int u, v, w;
    edge(int u, int v, int w) : u(u), v(v), w(w){};
};

vector<edge> g;
int d[maxn];
int backup[maxn];
int inqueue[maxn];
queue<int> q;

void addedge(int u, int v, int w) { g.push_back(edge(u, v, w)); }

void init() { memset(d, 0x3f, sizeof(d)); }

// void spfa(int s) {
//     d[s] = 0;
//     q.push(s);
//     inqueue[s] = 1;
//     while (!q.empty()) {
//         int u = q.front();
//         q.pop();
//         inqueue[u] = 0;
//         for (int i = 0; i < g[u].size(); i++) {
//             edge e = g[u][i];
//             if (d[e.v] > d[u] + e.w) {
//                 d[e.v] = d[u] + e.w;
//                 if (!inqueue[e.v]) {
//                     q.push(e.v);
//                     inqueue[e.v] = 1;
//                 }
//             }
//         }
//     }
// }

int bellman_ford(int s, int k, int n, int m) {
    // s源节点，k不超过的边数，n总节点数，m总边数
    d[s] = 0;
	// 最多k条边 限制循环k次
    for (int i = 0; i < k; i++) {
        // 备份数组
        memcpy(backup, d, sizeof(d));
        for (int j = 0; j < m; j++) {
            edge e = g[j];
            if (d[e.v] > d[e.u] + e.w) {
                d[e.v] = backup[e.u] + e.w;
            }
        }
    }
    if (d[n] > inf / 2)
        return -1;
    /*这里不像Dijkstra写等于正无穷是因为可能有负权边甚至是负环的存在，
    使得“正无穷”在迭代过程中受到一点影响。*/
    return d[n];
}

int main() {
    int n, m, k;
    cin >> n >> m >> k;
    int u, v, w;
    init();
    for (int i = 0; i < m; i++) {
        cin >> u >> v >> w;
        addedge(u, v, w);
    }
    int ans = bellman_ford(1, k, n, m);
    if (ans != -1)
        cout << d[n];
    else
        cout << "impossible";
    return 0;
}
```
# AcWing 算法基础课 -- 搜索与图论

## AcWing 847. 图中点的层次 

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环。

所有边的长度都是1，点的编号为1~n。

请你求出1号点到n号点的最短距离，如果从1号点无法走到n号点，输出-1。

**输入格式**

第一行包含两个整数n和m。

接下来m行，每行包含两个整数a和b，表示存在一条从a走到b的长度为1的边。

**输出格式**

输出一个整数，表示1号点到n号点的最短距离。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

4 5
1 2
2 3
3 4
1 3
1 4

输出样例：

1
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5 + 5;

struct Edge {
    int u, v;
    Edge(int u, int v) : u(u), v(v){};
};

vector<Edge> g[maxn];
queue<int> q;
int vis[maxn];
int d[maxn];

void addedge(int u, int v) { g[u].push_back(Edge(u, v)); }

void bfs(int s) {
    q.push(s);
    vis[s] = 1;
    d[s] = 0;
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        for (int i = 0; i < g[u].size(); i++) {
            Edge e = g[u][i];
            if (!vis[e.v]) {
                d[e.v] = d[u] + 1;
                q.push(e.v);
                vis[e.v] = 1;
            }
        }
    }
}

int main() {
    int n, m;
    cin >> n >> m;
    memset(d, 0x3f, sizeof(d));
    int u, v;
    for (int i = 0; i < m; i++) {
        cin >> u >> v;
        addedge(u, v);
    }
    bfs(1);
    cout << (d[n] == 0x3f3f3f3f ? -1 : d[n]);
    return 0;
}
```
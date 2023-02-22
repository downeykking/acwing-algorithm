# AcWing 算法基础课 -- 搜索与图论

## AcWing 860. 染色法判定二分图 

`难度：简单`

### 题目描述

给定一个n个点m条边的无向图，图中可能存在重边和自环。

请你判断这个图是否是二分图。

**输入格式**

第一行包含两个整数n和m。

接下来m行，每行包含两个整数u和v，表示点u和点v之间存在一条边。

**输出格式**

如果给定图是二分图，则输出“Yes”，否则输出“No”。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

4 4
1 3
1 4
2 3
2 4

输出样例：

Yes
```

### Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5 + 5;

struct Edge {
    int u, v;
    Edge(int u, int v) : u(u), v(v){};
};

vector<Edge> g[maxn];
int color[maxn]; // -1没染色 1黑 0白

void addedge(int u, int v) { g[u].push_back(Edge(u, v)); }

bool dfs(int u, int c) {
    color[u] = c;
    for (int i = 0; i < g[u].size(); i++) {
        Edge e = g[u][i];
        if (color[e.v] == -1) {
            if (!dfs(e.v, !c))
                return false;
        }
        else if (color[e.v] == c)
            return false;
    }
    return true;
}

int main() {
    int n, m;
    cin >> n >> m;
    int u, v;
    for (int i = 0; i < m; i++) {
        cin >> u >> v;
        addedge(u, v);
        addedge(v, u);
    }
    memset(color, -1, sizeof(color));
    bool flag = true;
    for (int i = 1; i <= n; i++)
        if (color[i] == -1)
            if (!dfs(i, 0)) {
                flag = false;
                break;
            }
    if (flag)
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```
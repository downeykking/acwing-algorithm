# AcWing 算法基础课 -- 搜索与图论

## AcWing 858. Prim算法求最小生成树 

`难度：简单`

### 题目描述

给定一个n个点m条边的无向图，图中可能存在重边和自环，边权可能为负数。

求最小生成树的树边权重之和，如果最小生成树不存在则输出impossible。

给定一张边带权的无向图G=(V, E)，其中V表示图中点的集合，E表示图中边的集合，n=|V|，m=|E|。

由V中的全部n个顶点和E中n-1条边构成的无向连通子图被称为G的一棵生成树，其中边的权值之和最小的生成树被称为无向图G的最小生成树。

**输入格式**

第一行包含两个整数n和m。

接下来m行，每行包含三个整数u，v，w，表示点u和点v之间存在一条权值为w的边。

**输出格式**

共一行，若存在最小生成树，则输出一个整数，表示最小生成树的树边权重之和，如果最小生成树不存在则输出impossible。

**数据范围**

$1≤n≤500,$
$1≤m≤105,$
图中涉及边的边权的绝对值均不超过10000。

```r
输入样例：

4 5
1 2 1
1 3 2
1 4 3
2 3 2
3 4 4

输出样例：

6
```

### Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 500 + 5;
const int inf = 0x3f3f3f3f;

int g[maxn][maxn];
int d[maxn];
int intree[maxn];

void init(int n) {
    memset(d, 0x3f, sizeof(d));
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= n; j++) {
            if (i == j)
                g[i][j] = 0;
            else {
                g[i][j] = inf;
            }
        }
    }
}

int prim(int n) {
    int res = 0;
    d[1] = 0;
    for (int i = 0; i < n; i++) {
        int t = -1;
        for (int j = 1; j <= n; j++) {
            if (!intree[j] && ((t == -1) || d[j] < d[t])) {
                t = j;
            }
        }

        if (d[t] == inf)
            return inf;
        res += d[t];
        intree[t] = 1;

        for (int j = 1; j <= n; j++) {
            d[j] = min(d[j], g[t][j]);
        }
    }
    return res;
}

int main() {
    int n, m;
    cin >> n >> m;
    init(n);
    int u, v, w;
    for (int i = 0; i < m; i++) {
        cin >> u >> v >> w;
        g[u][v] = min(g[u][v], w);
        g[v][u] = min(g[v][u], w);
    }
    int res = prim(n);
    if (res == inf)
        cout << "Impossible";
    else
        cout << res;
    return 0;
}
```
# AcWing 算法基础课 -- 搜索与图论

## AcWing 

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

$1≤n≤10^5,$
$1≤m≤2∗10^5,$
图中涉及边的边权的绝对值均不超过1000。

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

const int maxn = 1e5 + 5;
const int maxm = 2e5 + 5;

int fa[maxn];

int find(int x) { return x == fa[x] ? x : (fa[x] = find(fa[x])); }

struct Edge {
    int u, v, w;
    bool operator<(const Edge &e) const { return w < e.w; }
};

Edge edges[maxm];

int main() {
    int n, m;
    cin >> n >> m;
    for (int i = 1; i <= n; i++)
        fa[i] = i;
    int u, v, w;
    for (int i = 0; i < m; i++) {
        cin >> edges[i].u >> edges[i].v >> edges[i].w;
    }
    sort(edges, edges + n);
    int cnt = 0, res = 0;
    for (int i = 0; i < m; i++) {
        u = edges[i].u, v = edges[i].v, w = edges[i].w;
        int a = find(u), b = find(v);
        if (a != b) {
            fa[a] = b;
            res += w;
            cnt++;
        }
    }
    // 节点个数减1
    if (cnt == n - 1)
        cout << res;
    else
        cout << "Impossible";
    return 0;
}
```
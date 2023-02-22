# AcWing 算法基础课 -- 搜索与图论

## AcWing 854. Floyd求最短路 

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，图中可能存在重边和自环，边权可能为负数。

再给定k个询问，每个询问包含两个整数x和y，表示查询从点x到点y的最短距离，如果路径不存在，则输出“impossible”。

数据保证图中不存在负权回路。

**输入格式**

第一行包含三个整数n，m，k

接下来m行，每行包含三个整数x，y，z，表示存在一条从点x到点y的有向边，边长为z。

接下来k行，每行包含两个整数x，y，表示询问点x到点y的最短距离。

**输出格式**

共k行，每行输出一个整数，表示询问的结果，若询问两点间不存在路径，则输出“impossible”。

**数据范围**

$1≤n≤200,$
$1≤k≤n^2$
$1≤m≤20000,$
图中涉及边长绝对值均不超过10000。

```r
输入样例：

3 3 2
1 2 1
2 3 2
1 3 1
2 1
1 3

输出样例：

impossible
1
```

### Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 200 + 5;
const int inf = 0x3f3f3f3f;

int g[maxn][maxn];

int n, m, k;

void init() {
    for (int i = 1; i <= n; i++)
        for (int j = 1; j <= n; j++)
            if (i == j)
                g[i][j] = 0;
            else
                g[i][j] = inf;
}

void floyd() {
    for (int k = 1; k <= n; k++) {
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= n; j++) {
                g[i][j] = min(g[i][j], g[i][k] + g[k][j]);
            }
        }
    }
}

int main() {
    cin >> n >> m >> k;
    int u, v, w;
    init();
    for (int i = 0; i < m; i++) {
        cin >> u >> v >> w;
        g[u][v] = min(g[u][v], w);
    }
    floyd();
    for (int i = 0; i < k; i++) {
        cin >> u >> v;
        if (g[u][v] > inf / 2)
            cout << "impossible";
        else
            cout << g[u][v];
    }
    return 0;
}
```
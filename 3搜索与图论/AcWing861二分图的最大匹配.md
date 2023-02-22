# AcWing 算法基础课 -- 搜索与图论

## AcWing 861. 二分图的最大匹配 

`难度：简单`

### 题目描述

给定一个二分图，其中左半部包含n1个点（编号$1 \sim n1$），右半部包含n2个点（编号$1\sim n2$），二分图共包含m条边。

数据保证任意一条边的两个端点都不可能在同一部分中。

请你求出二分图的最大匹配数。

> 二分图的匹配：给定一个二分图G，在G的一个子图M中，M的边集{E}中的任意两条边都不依附于同一个顶点，则称M是一个匹配。
> 
> 二分图的最大匹配：所有匹配中包含边数最多的一组匹配被称为二分图的最大匹配，其边数即为最大匹配数。

**输入格式**

第一行包含三个整数 n1、n2 和 m。

接下来m行，每行包含两个整数u和v，表示左半部点集中的点u和右半部点集中的点v之间存在一条边。

**输出格式**

输出一个整数，表示二分图的最大匹配数。

**数据范围**

$1≤n1,n2≤500,$
$1≤u≤n1,$
$1≤v≤n2,$
$1≤m≤10^5$

```r
输入样例：

2 2 4
1 1
1 2
2 1
2 2

输出样例：

2
```

### Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 500 + 5;
int n1, n2, m;

vector<int> g[maxn];
int p[maxn];
int vis[maxn];

bool match(int u) {
    for (int j = 0; j < g[u].size(); j++) {
        int v = g[u][j];
        if (!vis[v]) {
            vis[v] = 1;
            if (p[v] == 0 || match(p[v])) {
                p[v] = u;
                return true;
            }
        }
    }
    return false;
}

int main() {
    cin >> n1 >> n2 >> m;
    int u, v;
    for (int i = 0; i < m; i++) {
        cin >> u >> v;
        g[u].push_back(v);
    }
    int cnt = 0;
    for (int i = 1; i <= n1; i++) {
        memset(vis, 0, sizeof(vis));
        if (match(i))
            cnt++;
    }
    cout << cnt;
    return 0;
}
```
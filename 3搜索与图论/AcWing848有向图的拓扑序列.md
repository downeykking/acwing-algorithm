# AcWing 算法基础课 -- 搜索与图论

## AcWing 848. 有向图的拓扑序列 

`难度：简单`

### 题目描述

给定一个n个点m条边的有向图，点的编号是1到n，图中可能存在重边和自环。

请输出任意一个该有向图的拓扑序列，如果拓扑序列不存在，则输出-1。

若一个由图中所有点构成的序列A满足：对于图中的每条边(x, y)，x在A中都出现在y之前，则称A是该图的一个拓扑序列。

**输入格式**

第一行包含两个整数n和m

接下来m行，每行包含两个整数x和y，表示存在一条从点x到点y的有向边(x, y)。

**输出格式**

共一行，如果存在拓扑序列，则输出任意一个合法的拓扑序列即可。

否则输出-1。

**数据范围**

$1≤n,m≤10^5$

```
输入样例：

3 3
1 2
2 3
1 3

输出样例：

1 2 3
```

### Solution

有向无环图也叫拓扑图

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e4 + 5;

struct edge {
    int u, v;
    edge(int u, int v) : u(u), v(v){};
};

vector<edge> g[maxn];
queue<int> q;
int dg[maxn][maxn];
int d[maxn];
vector<int> ans;

void addedge(int u, int v) { g[u].push_back(edge(u, v)); }

int topo(int n) {
    int cnt = 0;
    for (int i = 1; i <= n; i++) {
        if (d[i] == 0)
            q.push(i);
    }
    while (!q.empty()) {
        int now = q.front();
        q.pop();
        cnt++;
        ans.push_back(now);
        for (int i = 1; i <= n; i++) {
            if (dg[now][i]) {
                d[i]--;
                if (d[i] == 0)
                    q.push(i);
            }
            
        }
    }
    return cnt == n;
}

int main() {
    int n, m;
    cin >> n >> m;
    int u, v;
    for (int i = 0; i < m; i++) {
        cin >> u >> v;
        if (!dg[u][v]) {
            dg[u][v] = 1;
            d[v]++;
        }
    }
    if (topo(n))
        for (int num : ans)
            cout << num << " ";
    else
        cout << -1;
}

```
# AcWing 算法基础课 -- 搜索与图论

## AcWing 852. spfa判断负环

`难度：简单`

### 题目描述

给定一个 n 个点 m条边的有向图，图中可能存在重边和自环， 边权可能为负数。
请你判断图中是否存在负权回路。

**输入格式**

第一行包含整数 n 和 m。

接下来 m行每行包含三个整数 x,y,z，表示存在一条从点 x 到点 y 的有向边，边长为 z

**输出格式**

如果图中存在负权回路，则输出 Yes，否则输出 No。

**数据范围**

$1≤n≤2000,$
$1≤m≤10000,$

任意边长的绝对值不超过10000。

```r
输入样例：

3 3
1 2 -1
2 3 4
3 1 -4

输出样例：

Yes
```

### Solution

spfa加cnt数组来判断入队次数是否大于n

```java
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5 + 5;
const int inf = 0x3f3f3f3f;
struct edge {
    int u, v, w;
    edge(int u, int v, int w) : u(u), v(v), w(w){};
};

vector<edge> g[maxn];
int d[maxn];
int cnt[maxn];
int inqueue[maxn];
queue<int> q;

void addedge(int u, int v, int w) { g[u].push_back(edge(u, v, w)); }

// 这里的距离数组d无需初始化的，一开始就是0，表示自己到自己的最短路是0（或者表示这些点到超级源点的距离是0）
void init() { memset(d, 0, sizeof(d)); }

bool spfa(int n) {
    //负环从1号点不一定能到达，我们将所有点压入队列作为初始点集
    for (int i = 1; i <= n; i ++ ) {
		inqueue[i] = 1;
		q.push(i);
	} 
    while (!q.empty()) {
        int u = q.front();
        q.pop();
        inqueue[u] = 0;
        for (int i = 0; i < g[u].size(); i++) {
            edge e = g[u][i];
            if (d[e.v] > d[u] + e.w) {
                d[e.v] = d[u] + e.w;
                cnt[e.v] = cnt[e.u]+1;
                if(cnt[e.v]>=n)
                    return true;
                if (!inqueue[e.v]) {
                    q.push(e.v);
                    inqueue[e.v] = 1;
                    
                }
            }
        }
    }
    return false;
}


int main() {
    int n, m;
    cin >> n >> m;
    int u, v, w;
    init();
    for (int i = 0; i < m; i++) {
        cin >> u >> v >> w;
        addedge(u, v, w);
    }
    if(spfa(n))
        cout<<"Yes";
    else
        cout << "No";
    return 0;
}
```
# AcWing 算法基础课 -- 搜索与图论

## AcWing 844. 走迷宫  

`难度：简单`

### 题目描述

给定一个n*m的二维整数数组，用来表示一个迷宫，数组中只包含0或1，其中0表示可以走的路，1表示不可通过的墙壁。

最初，有一个人位于左上角(1, 1)处，已知该人每次可以向上、下、左、右任意一个方向移动一个位置。

请问，该人从左上角移动至右下角(n, m)处，至少需要移动多少次。

数据保证(1, 1)处和(n, m)处的数字为0，且一定至少存在一条通路。

**输入格式**

第一行包含两个整数n和m。

接下来n行，每行包含m个整数（0或1），表示完整的二维数组迷宫。

**输出格式**

输出一个整数，表示从左上角移动至右下角的最少移动次数。

**数据范围**

$1≤n,m≤100$

```r
输入样例：

5 5
0 1 0 0 0
0 1 0 1 0
0 0 0 0 0
0 1 1 1 0
0 0 0 1 0

输出样例：

8
```
### Solution

方法1：需要用vis数组标记是否访问

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 103;
int n, m;

int g[maxn][maxn];
int vis[maxn][maxn];
struct node {
    int x, y, d;
    node(int x, int y, int d) : x(x), y(y), d(d){};
};

queue<node> q;

int dx[4] = {-1, 0, 0, 1};
int dy[4] = {0, -1, 1, 0};

void bfs(int sx, int sy) {
    q.push(node(sx, sy, 0));
    while (!q.empty()) {
        node now = q.front();
        q.pop();
        if(now.x==n&&now.y==m){
        	cout<<now.d;
        	return;
        }
        for (int i = 0; i < 4; i++) {
            int nx = dx[i] + now.x;
            int ny = dy[i] + now.y;
            if (nx >= 1 && nx <= n && ny >= 1 && ny <= m && g[nx][ny] == 0 && vis[nx][ny]==0) {
                q.push(node(nx, ny, now.d+1));
                vis[nx][ny] = 1;
            }
        }
    }
}

int main() {
    cin >> n >> m;
    int sx = 1;
    int sy = 1;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            cin >> g[i][j];
        }
    }
    bfs(1, 1);
}
```

方法2：用d距离数组来代替是否访问

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 103;
int n, m;

int g[maxn][maxn];
int d[maxn][maxn];
typedef pair<int, int> pii;

queue<pii> q;

int dx[4] = {-1, 0, 0, 1};
int dy[4] = {0, -1, 1, 0};

void bfs(int sx, int sy) {
    q.push({sx, sy});
    d[sx][sy] = 1;
    while (!q.empty()) {
        pii now = q.front();
        q.pop();
       	if(now.first==n&&now.second==m){
        	cout<<d[now.first][now.second]-1;
        	return;
        }
        for (int i = 0; i < 4; i++) {
            int nx = dx[i] + now.first;
            int ny = dy[i] + now.second;
            if (nx >= 1 && nx <= n && ny >= 1 && ny <= m && g[nx][ny] == 0 &&
                d[nx][ny] == 0) {
                q.push({nx, ny});
                d[nx][ny] = d[now.first][now.second] + 1;
            }
            if (nx == n && ny == m) {
                cout << d[nx][ny] - 1;
                return;
            }
        }
    }
}

int main() {
    cin >> n >> m;
    int sx = 1;
    int sy = 1;
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= m; j++) {
            cin >> g[i][j];
        }
    }
    bfs(1, 1);
}
```






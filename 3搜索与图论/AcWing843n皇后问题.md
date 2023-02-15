# AcWing 算法基础课 -- 搜索与图论

## AcWing 843. n-皇后问题 

`难度：中等`

### 题目描述

n-皇后问题是指将 n 个皇后放在 n∗n 的国际象棋棋盘上，使得皇后不能相互攻击到，即任意两个皇后都不能处于同一行、同一列或同一斜线上。

现在给定整数n，请你输出所有的满足条件的棋子摆法。

**输入格式**

共一行，包含整数n。

**输出格式**

每个解决方案占n行，每行输出一个长度为n的字符串，用来表示完整的棋盘状态。

其中”.”表示某一个位置的方格状态为空，”Q”表示某一个位置的方格上摆着皇后。

每个方案输出完成后，输出一个空行。

输出方案的顺序任意，只要不重复且没有遗漏即可。

**数据范围**

$1≤n≤9$

```r
输入样例：

4

输出样例：

.Q..
...Q
Q...
..Q. 

..Q.
Q...
...Q
.Q..
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 10;
int n, k;

bool check(int row, int col, vector<vector<char>> &g) {
    // 检查右上方是否有皇后互相冲突
    for (int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++) {
        if (g[i][j] == 'Q')
            return false;
    }
    // 检查左上方是否有皇后互相冲突
    for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
        if (g[i][j] == 'Q')
            return false;
    }

    for (int k = 0; k <= row; k++) {
        if (g[k][col] == 'Q')
            return false;
    }
    return true;
}

void dfs(int x, int cnt, vector<vector<char>> &g) {
    if (cnt == n) {
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                cout << g[i][j];
            }
            cout << endl;
        }
        cout<<endl;
        return;
    }
    for (int i = 0; i < n; i++) {
        // 减枝
        if (!(check(x, i, g)))
            continue;
        g[x][i] = 'Q';
        dfs(x + 1, cnt + 1, g);
        g[x][i] = '.';
    }
}

int main() {
    cin >> n;
    vector<vector<char>> g(n, vector<char>(n, '.'));
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            cout << g[i][j];
        }
        cout << endl;
    }
    dfs(0, 0, g);
    return 0;
}

```
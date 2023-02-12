# AcWing 算法基础课 -- 数据结构

## AcWing 836. 合并集合

`难度：简单`

### 题目描述

一共有n个数，编号是1~n，最开始每个数各自在一个集合中。

现在要进行m个操作，操作共有两种：

-  “M a b”，将编号为a和b的两个数所在的集合合并，如果两个数已经在同一个集合中，则忽略这个操作；
-  “Q a b”，询问编号为a和b的两个数是否在同一个集合中；

**输入格式**

第一行输入整数n和m。

接下来m行，每行包含一个操作指令，指令为“M a b”或“Q a b”中的一种。

**输出格式**

对于每个询问指令”Q a b”，都要输出一个结果，如果a和b在同一集合内，则输出“Yes”，否则输出“No”。

每个结果占一行。

**数据范围**

$1≤n,m≤10^5$

```r
输入样例：

4 5
M 1 2
M 3 4
Q 1 2
Q 1 3
Q 3 4

输出样例：

Yes
No
Yes
```

### Solution

并查集结构：1. 快速合并两个集合，快速查询两个元素是否在同一个集合中

注意 `find(int x)` 函数中的路径压缩 `p[x] = find[x]`

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 100010;
int fa[N];

void init(int n) {
    for (int i = 1; i <= n; i++)
        fa[i] = i;
}

int find(int x) { return fa[x] == x ? x : (fa[x] = find(fa[x])); }

int main() {
    int n, m;
    cin >> n >> m;
    init(n);
    char op;
    int a, b;
    for (int i = 0; i < m; i++) {
        cin >> op >> a >> b;
        if (op == 'Q') {
            if (find(a) == find(b))
                cout << "Yes" << endl;
            else
                cout << "No" << endl;
        }
        if (op == 'M') {
            fa[find(a)] = find(b);
        }
    }
    return 0;
}
```
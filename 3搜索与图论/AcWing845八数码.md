# AcWing 算法基础课 -- 搜索与图论

## AcWing 845. 八数码

`难度：简单`

### 题目描述

在一个3×3的网格中，1~8这8个数字和一个“x”恰好不重不漏地分布在这3×3的网格中。

例如：

```r
1 2 3
x 4 6
7 5 8
```

在游戏过程中，可以把“x”与其上、下、左、右四个方向之一的数字交换（如果存在）。

我们的目的是通过交换，使得网格变为如下排列（称为正确排列）：

```r
1 2 3
4 5 6
7 8 x
```

例如，示例中图形就可以通过让“x”先后与右、下、右三个方向的数字交换成功得到正确排列。

交换过程如下：

```r
1 2 3   1 2 3   1 2 3   1 2 3
x 4 6   4 x 6   4 5 6   4 5 6
7 5 8   7 5 8   7 x 8   7 8 x
```

现在，给你一个初始网格，请你求出得到正确排列至少需要进行多少次交换。


**输入格式**

输入占一行，将3×3的初始网格描绘出来。

例如，如果初始网格如下所示：

```r
1 2 3

x 4 6

7 5 8

则输入为：1 2 3 x 4 6 7 5 8
```

**输出格式**

输出占一行，包含一个整数，表示最少交换次数。

如果不存在解决方案，则输出”-1”。

```r
输入样例：

2  3  4  1  5  x  7  6  8 

输出样例

19
```

### Solution

字符串处理差劲，这部分还要优化。

```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 103;

unordered_map<string, int> umap;
typedef pair<string, int> psi;

queue<psi> q;

int dx[4] = {-1, 0, 0, 1};
int dy[4] = {0, -1, 1, 0};

int bfs(string s, int idx) {
    q.push({s, idx});
    umap[s] = 0;
    while (!q.empty()) {
        psi now = q.front();
        q.pop();
        s = now.first;
        idx = now.second;
        int d = umap[s];
        if (s == "12345678x")
            return d;
        int row = idx / 3;
        int col = idx % 3;
        
        for (int i = 0; i < 4; i++) {
            int nx = dx[i] + row;
            int ny = dy[i] + col;
            if (nx >= 0 && nx < 3 && ny >= 0 && ny < 3) {
                int idx_n = nx * 3 + ny;
                swap(s[idx_n], s[idx]);
                if (s == "12345678x")
                    return d + 1;
                // 防止重复入队
                if (umap[s] == 0) {
                    q.push({s, idx_n});
                    umap[s] = d + 1;
                }
                swap(s[idx_n], s[idx]);
            }
        }
    }
    return -1;
}

int main() {
    string str;
    getline(cin, str);
    int index = 0;
    while ((index = str.find(' ', index)) != string::npos) {
        str.erase(index, 1);
    }
    int ans = bfs(str, str.find('x'));
    cout << ans;
    return 0;
}
```
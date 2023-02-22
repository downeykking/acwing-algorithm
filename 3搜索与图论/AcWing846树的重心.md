# AcWing 算法基础课 -- 搜索与图论

## AcWing 846. 树的重心 

`难度：简单`

### 题目描述

给定一颗树，树中包含n个结点（编号1~n）和n-1条无向边。

请你找到树的重心，并输出将重心删除后，剩余各个连通块中点数的最大值。

重心定义：重心是指树中的一个结点，如果将这个点删除后，剩余各个连通块中点数的最大值最小，那么这个节点被称为树的重心。

**输入格式**

第一行包含整数n，表示树的结点数。

接下来n-1行，每行包含两个整数a和b，表示点a和点b之间存在一条边。

**输出格式**

输出一个整数m，表示将重心删除后，剩余各个连通块中点数的最大值。

**数据范围**

$1≤n≤10^5$

```r
输入样例

9
1 2
1 7
1 4
2 8
2 5
4 3
3 9
4 6

输出样例：

4
```

### Solution

```java
import java.util.*;
import java.io.*;

class Main{
    public static final int N = 100010;
    // 因为是无向边，所以要乘以 2
    public static int[] e = new int[N * 2];
    public static int[] ne = new int[N * 2];
    public static int[] h = new int[N * 2];
    // idx 初始化为 1，这样指向 0 的时候就代表为空
    public static int idx = 1;
    // 标记该点是否遍历过
    public static boolean[] flag = new boolean[N];
    // 记录答案,求最小值，初始化为最大
    public static int ans = N;
    public static void main(String[] args) throws IOException{
        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
        int n = Integer.parseInt(br.readLine());
        String[] s;
        for(int i = 1; i <= n - 1; i++){
            s = br.readLine().split(" ");
            int a = Integer.parseInt(s[0]);
            int b = Integer.parseInt(s[1]);
            // 建树
            add(a, b);
            add(b, a);
        }
        // 数据范围 1-100000，所以从 1 开始递归
        dfs(1, n);
        System.out.println(ans);
    }
    public static void add(int a, int b){
        e[idx] = b;
        ne[idx] = h[a];
        h[a] = idx;
        idx++;
    }
    public static int dfs(int u, int n){
        flag[u] = true;
        int size = 0, sum = 0;
        for(int i = h[u]; i != 0; i = ne[i]){
            int j = e[i];
            if(flag[j]) continue;
            int s = dfs(j, n);
            // 找到子树中点数最多的
            size = Math.max(size, s);
            // 计算所有子树的点数的和
            sum += s;
        }
        // 在子树和子树外求一个最大值
        size = Math.max(size, n - sum - 1);
        // 求答案
        ans = Math.min(ans, size);
        return sum + 1;
    }
}
```



```cpp
#include <bits/stdc++.h>
using namespace std;

const int maxn = 1e5 + 10;
int n;
bool st[maxn];
int sz[maxn];
int ans; // 设置一个全局的答案，存储“最小的最大值”

vector<int> g[maxn];

int dfs(int u) // 返回以 u 为子树的大小
{
    int res = 0; // 存储将该点删去之后，剩余各连通块大小的最大值
    sz[u] = 1; // 当前点算 1 个点，所以从 1 开始
    st[u] = true;
    for (int i = 0; i < g[u].size(); i++) {
        int j = g[u][i];
        if (!st[j]) {
            int s = dfs(j); // 子树 j 大小
            res = max(res, s); // 子树 j 是个连通块，将它的大小与 res 取 max
            sz[u] += s; // 子树 j 是子树 u 的一部分，因此 sz[u] 要加上子树 j
                        // 大小
        }
    }
    res = max(res, n - sz[u]); // n-sz[u] 即上文提到的节点 u “父节点及以上部分”
                               // 的大小，也是个连通块，用其大小更新 res
    ans = min(ans, res); // 更新全局答案
    return sz[u];
}

int main() {
    cin >> n;
    ans = n;
    for (int i = 0; i < n - 1; ++i) {
        int a, b;
        scanf("%d%d", &a, &b);
        // 无向边
        g[a].push_back(b);
        g[b].push_back(a);
    }
    dfs(1);
    printf("%d\n", ans);
    return 0;
}
```


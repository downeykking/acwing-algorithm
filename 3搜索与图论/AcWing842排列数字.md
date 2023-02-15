# AcWing 算法基础课 -- 搜索与图论
## AcWing 842. 排列数字 

`难度：简单`

### 题目描述

给定一个整数n，将数字1~n排成一排，将会有很多种排列方法。

现在，请你按照字典序将所有的排列方法输出。

**输入格式**

共一行，包含一个整数n。

**输出格式**

按字典序输出所有排列方案，每个方案占一行。

**数据范围**

$1≤n≤7$

```r
输入样例：

3

输出样例：

1 2 3
1 3 2
2 1 3
2 3 1
3 1 2
3 2 1
```

### Solution

```cpp
#include <bits/stdc++.h>
using namespace std;

const int N = 10;
vector<vector<int>> ans;

int n, k;
void dfs(int i, vector<int> &temp, vector<int> &vis) {
    if (temp.size() >= n) {
        ans.push_back(temp);
        return;
    }

    for (int j = 1; j <= n; j++) {
        if(vis[j])
            continue;
        temp.push_back(j);
        vis[j] = 1;
        dfs(i+1, temp, vis);
        temp.pop_back();
        vis[j] = 0;
    }
}

int main() {
    cin >> n;

    vector<int> temp;
    vector<int> vis(n, 0);
    dfs(1, temp, vis);
    for (int i = 0; i < ans.size(); i++) {
        for (int j = 0; j < ans[i].size(); j++) {
            cout << ans[i][j] << " ";
        }
        cout << endl;
    }
    return 0;
}
```
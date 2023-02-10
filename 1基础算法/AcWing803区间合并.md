# AcWing 算法基础课 -- 基础算法

## AcWing 803. 区间合并 

`难度：简单`

### 题目描述

给定 n 个区间 $[l_i,r_i]$，要求合并所有有交集的区间。

注意如果在端点处相交，也算有交集。

输出合并完成后的区间个数。

例如：[1,3]和[2,6]可以合并为一个区间[1,6]。

**输入格式**

第一行包含整数n。

接下来n行，每行包含两个整数 l 和 r。

**输出格式**

共一行，包含一个整数，表示合并区间完成后的区间个数。

**数据范围**:

$1≤n≤100000,$
$−10^9≤l_i≤r_i≤10^9$

```r
输入样例：

5
1 2
2 4
5 6
7 8
7 9

输出样例：

3
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;

typedef pair<int, int> pii;
vector<pii> a;

int main() {
    int n, l, r;
    cin >> n;
    for(int i=0;i<n;i++) {
        cin >> l >> r;
        a.push_back({l, r});
    }
    // 左升序排列
    sort(a.begin(), a.end());
    int ans = 1;
    int first = a[0].first;
    int end = a[0].second;

    for (int i = 1; i < n; i++) {
        pii curr = a[i];
        if (curr.first > end) {
            ans++;
            end = curr.second;
        } else {
            end = max(curr.second, end);
        }
    }
    cout << ans;
    return 0;
}
```


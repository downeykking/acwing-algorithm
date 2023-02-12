# AcWing 算法基础课 -- 数据结构

## AcWing 143. 最大异或对

`难度：简单`

### 题目描述

在给定的N个整数A1，A2……AN

中选出两个进行xor（异或）运算，得到的结果最大是多少？

**输入格式**

第一行输入一个整数N。

第二行输入N个整数A1～AN。

**输出格式**

输出一个整数表示答案。

**数据范围**

$1≤N≤10^5,$
$0≤Ai<2^31$

```r
输入样例：

3
1 2 3

输出样例：

3
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e5 + 10;
int a[N], son[N * 31][2], idx; //[N*31] N个数据 每个数据占31位 [2] 0 1两种情况

void insert(int x) {
    int p = 0;                    // 根节点出发
    for (int i = 30; i >= 0; i--) // x用31位二进制表示
    {
        int k = x >> i & 1; // 将二进制从高位到低位输出
        if (son[p][k] == 0)
            son[p][k] = ++idx; // 如果查询的时候下面没有，就插入
        p = son[p][k];         // 往下搜
    }
}

int query(int x) {
    int p = 0, ans = 0;
    for (int i = 30; i >= 0; i--) {
        int k = x >> i & 1;
        if (son[p][!k]) // 看看相反位是否存在 0的相反位1 1的相反位0
        {
            ans = ans * 2 + !k; // 二进制转为十进制：×2+加上每一位
            p = son[p][!k];     // 向下搜
        }
        else // 不存在相反位，只能不情愿向下搜
        {
            ans = ans * 2 + k;
            p = son[p][k];
        }
    }
    return ans;
}
int main() {
    int m;
    scanf("%d", &m);
    for (int i = 0; i < m; i++)
        scanf("%d", &a[i]);
    int ans = 0;
    for (int i = 0; i < m; i++) {
        insert(a[i]);             // 先插入
        int t = query(a[i]);      // 查询与之异或最大的数
        ans = max(ans, a[i] ^ t); // 异或一下与答案比较，取最大值
    }
    printf("%d\n", ans);
    return 0;
}

```
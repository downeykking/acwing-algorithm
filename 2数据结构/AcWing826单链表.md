# AcWing 算法基础课 -- 数据结构

## AcWing 826. 单链表

`难度：简单`

### 题目描述

实现一个单链表，链表初始为空，支持三种操作：

(1) 向链表头插入一个数；

(2) 删除第k个插入的数后面的数；

(3) 在第k个插入的数后插入一个数

现在要对该链表进行M次操作，进行完所有操作后，从头到尾输出整个链表。

注意:题目中第k个插入的数并不是指当前链表的第k个数。例如操作过程中一共插入了n个数，则按照插入的时间顺序，这n个数依次为：第1个插入的数，第2个插入的数，…第n个插入的数。

**输入格式**

第一行包含整数M，表示操作次数。

接下来M行，每行包含一个操作命令，操作命令可能为以下几种：

(1) “H x”，表示向链表头插入一个数x。

(2) “D k”，表示删除第k个输入的数后面的数（当k为0时，表示删除头结点）。

(3) “I k x”，表示在第k个输入的数后面插入一个数x（此操作中k均大于0）。

**输出格式**

共一行，将整个链表从头到尾输出。

```r
数据范围

1≤M≤100000


所有操作保证合法。
输入样例：

10
H 9
I 1 1
D 1
D 0
H 6
I 3 6
I 4 5
I 4 5
I 3 4
D 6

输出样例：

6 4 6 5
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;

const int N = 1e6 + 10;
int e[N], ne[N], idx, head;

void init() {
    idx = 0;
    head = -1;
}

void addhead(int x) {
    e[idx] = x;
    ne[idx] = head;
    head = idx;
    idx++;
}

// 在第k个位置后面插入x
void insert(int k, int x) {
    e[idx] = x;
    ne[idx] = ne[k];
    ne[k] = idx;
    idx++;
}

// 删除第k个位置后面的数
void remove(int k) {
    if (k == 0) {
        head = ne[head];
    }
    else {
        ne[k] = ne[ne[k]];
    }
}

int main() {
    int n;
    cin >> n;
    init();
    for (int i = 0; i < n; i++) {
        char s;
        cin >> s;
        if (s == 'H') {
            int x;
            cin >> x;
            addhead(x);
        }
        else if (s == 'D') {
            int k;
            cin >> k;
            if (k == 0)
                remove(0);
            else
                remove(k - 1);
        }
        else if (s == 'I') {
            int k, x;
            cin >> k >> x;
            insert(k - 1, x);
        }
    }
    for (int i = head; i != -1; i = ne[i]) {
        cout << e[i] << " ";
    }
    return 0;
}
```
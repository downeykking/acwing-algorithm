# AcWing 算法基础课 -- 数据结构

## AcWing 829. 模拟队列 

`难度：简单`

### 题目描述

实现一个队列，队列初始为空，支持四种操作：

(1) “push x” – 向队尾插入一个数x；

(2) “pop” – 从队头弹出一个数；

(3) “empty” – 判断队列是否为空；

(4) “query” – 查询队头元素。

现在要对队列进行M个操作，其中的每个操作3和操作4都要输出相应的结果。

**输入格式**

第一行包含整数M，表示操作次数。

接下来M行，每行包含一个操作命令，操作命令为”push x”，”pop”，”empty”，”query”中的一种。

**输出格式**

对于每个”empty”和”query”操作都要输出一个查询结果，每个结果占一行。

其中，”empty”操作的查询结果为“YES”或“NO”，”query”操作的查询结果为一个整数，表示队头元素的值。

```r
数据范围

1≤M≤100000,
1≤x≤109,

所有操作保证合法。
输入样例：

10
push 6
empty
query
pop
empty
push 3
push 4
pop
query
push 6

输出样例：

NO
6
YES
4
```

### Solution

```c++
#include <bits/stdc++.h>
using namespace std;
const int N = 1e5 + 10;
int q[N];

//[hh,tt]之间为队列
int hh = 0;  // 队头位置
int tt = -1; // 队尾位置
// 操作次数
int m;
// 操作方式
string s;

// 入队：队尾先往后移动一格，再放入要插入的数据
void push(int x) { q[++tt] = x; }
// 出队：队头往后移动一格
void pop() { hh++; }
//[hh,tt]代表队列区间，当tt>=hh时，队列非空
void empty() {
    if (tt >= hh)
        cout << "NO" << endl;
    else
        cout << "YES" << endl;
}
// hh指向队头，q[hh]指向队头元素
void query() { cout << q[hh] << endl; }

int main() {
    cin >> m;
    while (m--) {
        cin >> s;
        if (s == "push") {
            int x;
            cin >> x;
            push(x);
        }
        if (s == "pop") {
            pop();
        }
        if (s == "empty") {
            empty();
        }
        if (s == "query") {
            query();
        }
    }
}
```
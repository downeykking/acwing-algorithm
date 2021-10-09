# AcWing 算法基础课 -- 基础算法

## AcWing 793. 高精度乘法 

`难度：简单`

### 题目描述

给定两个正整数A和B，请你计算A * B的值。

**输入格式**

共两行，第一行包含整数A，第二行包含整数B。

**输出格式**

共一行，包含A * B的值。


数据范围

$1≤A的长度≤100000,$
$0≤B≤10000$

```r
输入样例：

2
3

输出样例：

6
```
### Solution1 大数乘小数

```java
// C = A * b, A >= 0, b >= 0
//A,B已倒序，返回C也是倒序
vector<int> mul(vector<int> &A, int b)
{
    vector<int> C;

    int t = 0;
    for (int i = 0; i < A.size() || t; i ++ )
    {
        if (i < A.size()) t += A[i] * b;
        C.push_back(t % 10);
        t /= 10;
    }

    while (C.size() > 1 && C.back() == 0) C.pop_back();

    return C;
}
```

#### Solution2 大数乘大数

```
#include <bits/stdc++.h>
using namespace std;
int a[100],b[100],c[100];

string bigmul(string s1,string s2){
    int len1 = s1.length();
    int len2 = s2.length();
    for(int i=0;i<len1;i++){
    	a[i] = s1[len1-1-i]-'0';
    }
    for(int i=0;i<len2;i++){
    	b[i] = s2[len2-1-i]-'0';
    }
    for(int i=0; i<len1; i++) {
        for(int j=0; j<len2; j++) {
            c[i+j]+=a[i]*b[j];
            c[i+j+1]+=c[i+j]/10;
            c[i+j]%=10;
    	}
    }
    int index=len1+len2;
    //删除前导零
    while(c[index]==0 && index>0)
    	index--;
    string ans;
    for(int i=index; i>=0; i--)
        ans+=c[i]+'0';
    return ans;
}

int main() {
    string s1,s2,t;
    cin>>s1>>s2;
    t = bigmul(s1,s2);
    cout<<t;
    return 0;
}
```


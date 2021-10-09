# AcWing 算法基础课 -- 基础算法

## AcWing 791. 高精度加法

`难度：简单`

### 题目描述

给定两个正整数，计算它们的和

**输入格式**

共两行，每行包含一个整数。

**输出格式**

共一行，包含所求的和。

**数据范围**：
```r
1≤整数长度≤100000
```
**输入样例**：

```r
12
23
```

**输出样例**：

```r
35
```

### Solution

1. 用BitInteger来处理

```java
import java.math.BigInteger;
import java.io.*;

public class Main {

    public static void main(String[] args) throws IOException {
        BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
        BigInteger a = new BigInteger(in.readLine());
        BigInteger b = new BigInteger(in.readLine());
        System.out.println(a.add(b));
        
    }

}
```

2. 用字符串形式

```java
#include <iostream>
#include <cstdio>
#include <cstring>
#include <string>
using namespace std;
const int maxn = 100;
int a[maxn];
int b[maxn];
int c[maxn];

string bigadd(string s1,string s2){
	string ans;
    int len1 = s1.length();
    int len2 = s2.length();
    for(int i=0;i<len1;i++){
        a[i] = s1[len1-1-i]-'0';
	}
    for(int i=0;i<len2;i++){
        b[i] = s2[len2-1-i]-'0';
    }
    int len3 = max(len1,len2);
    int carry=0;
    for(int i=0;i<len3;i++){
        int temp = a[i]+b[i]+carry;
        c[i] = temp%10;
        carry = temp/10;
    }
    if(carry>0)
    	c[len3++]=carry;
    for(int i=len3-1;i>=0;i--)
        ans+=c[i]+'0';
    return ans;
}
    
int main(){
    string s1,s2;
    cin>>s1;
    cin>>s2;
    cout<<bigadd(s1,s2);
    return 0;
}
```

3. 用数组存的方法

```
// C = A + B, A >= 0, B >= 0
//A,B已倒序，返回C也是倒序
vector<int> add(vector<int> &A, vector<int> &B)
{
    if (A.size() < B.size()) return add(B, A);

    vector<int> C;
    int t = 0;
    for (int i = 0; i < A.size(); i ++ )
    {
        t += A[i];
        //B数组不够的位数不是用0保存的时候
        if (i < B.size()) t += B[i];
        C.push_back(t % 10);
        t /= 10;
    }

    if (t) C.push_back(t);
    return C;
}
```

[989. 数组形式的整数加法](https://leetcode-cn.com/problems/add-to-array-form-of-integer/)


# AcWing 算法基础课 -- 基础算法

## AcWing 796. 子矩阵的和 

`难度：简单`

### 题目描述

输入一个n行m列的整数矩阵，再输入q个询问，每个询问包含四个整数x1, y1, x2, y2，表示一个子矩阵的左上角坐标和右下角坐标。

对于每个询问输出子矩阵中所有数的和。

**输入格式**

第一行包含三个整数n，m，q。

接下来n行，每行包含m个整数，表示整数矩阵。

接下来q行，每行包含四个整数x1, y1, x2, y2，表示一组询问。

**输出格式**

共q行，每行输出一个询问的结果。

```r
数据范围

1≤n,m≤1000,
1≤q≤200000,
1≤x1≤x2≤n,
1≤y1≤y2≤m,
−1000≤矩阵内元素的值≤1000

输入样例：

3 4 3
1 7 2 4
3 6 2 8
2 1 2 3
1 1 2 2
2 1 3 4
1 3 3 4

输出样例：

17
27
21
```

### Solution

```java
class NumMatrix {
public:
    vector<vector<int>> sum;
    NumMatrix(vector<vector<int>>& matrix) {
        int m = matrix.size();
        if(m==0)
            return;
        int n = matrix[0].size();
        if(n==0)
            return;
        vector<int> temp(n+1);
        sum.resize(m+1,temp);

        //sum从1开始 数从0开始
        for(int i=1;i<=m;i++){
            for(int j=1;j<=n;j++)
                sum[i][j] = sum[i-1][j] + sum[i][j-1] - sum[i-1][j-1] + matrix[i-1][j-1];
        }
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        row1++;col1++;row2++;col2++;
        return sum[row2][col2]- sum[row1-1][col2] -sum[row2][col1-1] +sum[row1-1][col1-1];
    }
};
```

[304. 二维区域和检索 - 矩阵不可变](https://leetcode-cn.com/problems/range-sum-query-2d-immutable/)
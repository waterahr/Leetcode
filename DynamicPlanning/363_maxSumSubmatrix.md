# 363.矩形区域不超过K的最大数值和

找不到合适的办法,就只好试一试暴力搜索了.但是在暴力之前,先用动态规划求得从坐标(0, 0)到(i, j)的矩形面积.

```cpp
class Solution {
public:
    int maxSumSubmatrix(vector<vector<int>>& matrix, int k) {
        int row = matrix.size(), col = matrix[0].size();
        vector<vector<int>> sum(row, vector<int>(col, 0));
        sum[0][0] = matrix[0][0];
        for(int i=1; i<col; i++)
            sum[0][i] = sum[0][i-1] + matrix[0][i];
        for(int j=1; j<row; j++)
            sum[j][0] = sum[j-1][0] + matrix[j][0];
        for(int i=1; i<row; i++)
            for(int j=1; j<col; j++)
                sum[i][j] = sum[i-1][j] + sum[i][j-1] - sum[i-1][j-1] + matrix[i][j];
        int res = INT_MIN;
        for(int i=0; i<row; i++)
            for(int j=0; j<col; j++)
                for(int m=i; m<row; m++)
                    for(int n=j; n<col; n++){
                        int area = sum[m][n];
                        if(i>=1)
                            area -= sum[i-1][n];
                        if(j>=1)
                            area -= sum[m][j-1];
                        if(i>=1 && j>=1)
                            area += sum[i-1][j-1];
                        if(area <= k){
                            res = max(res, area);
                            //cout<<i<<j<<m<<n;
                        }
                            
                    }
        return res;
    }
};
```

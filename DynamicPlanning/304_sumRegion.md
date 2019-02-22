# 304.二位区域和检索-矩阵不可变

dp[i][j]存储(0, 0)\~(i, j)区域内的数值和,递推关系式为:dp[i][j]=dp[i-1][j]+Sigma{nums[i][k]}(0<=k<=j).

```cpp
class NumMatrix {
public:
    NumMatrix(vector<vector<int>> matrix) {
        int m = matrix.size();
        if(m == 0) return ;
        int n = matrix[0].size();
        vector<vector<int>> dp(m, vector<int>(n, 0));
        for(int i=0; i<m; i++){
            int cur_row_sum = 0;
            for(int j=0; j<n; j++){
                cur_row_sum += matrix[i][j];
                if(i>0) dp[i][j] = dp[i-1][j];
                dp[i][j] += cur_row_sum;
            }
        }
        this->dp = dp;
    }
    
    int sumRegion(int row1, int col1, int row2, int col2) {
        if(dp.size()==0) return 0;
        int sum = dp[row2][col2];
        if(row1 > 0) sum -= dp[row1-1][col2];
        if(col1 > 0) sum -= dp[row2][col1-1];
        if(row1 > 0 && col1 > 0) sum += dp[row1-1][col1-1];
        return sum;
        
    }
    
private:
    vector<vector<int>> dp;
};

/**
 * Your NumMatrix object will be instantiated and called as such:
 * NumMatrix obj = new NumMatrix(matrix);
 * int param_1 = obj.sumRegion(row1,col1,row2,col2);
 */
```

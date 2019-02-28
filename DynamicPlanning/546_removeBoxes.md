# 546.移除盒子

dp[l][r][k]表示在boxes[l:r+1]之间有k个box的值等于boxes[r],状态转移方程为:
dp[l][r][k]=max(dp[l][i][k+1], dp[i+1][r-1][0])(boxes[i]==boxes[r]).

```cpp
class Solution {
public:
    int removeBoxes(vector<int>& boxes) {
        int n=boxes.size();
        int memo[100][100][100] = {0};
        return dfs(boxes,memo,0,n-1,0);
    }
    
private:
    int dfs(vector<int>& boxes,int memo[100][100][100], int l,int r,int k){
        if (l>r) return 0;
        if (memo[l][r][k]!=0) return memo[l][r][k];
 
        while (r>l && boxes[r]==boxes[r-1]) {r--;k++;}
        memo[l][r][k] = dfs(boxes,memo,l,r-1,0) + (k+1)*(k+1);
        for (int i=l; i<r; i++){
            if (boxes[i]==boxes[r]){
                memo[l][r][k] = max(memo[l][r][k], dfs(boxes,memo,l,i,k+1) + dfs(boxes,memo,i+1,r-1,0));
            }
        }
        return memo[l][r][k];
    }
};
```

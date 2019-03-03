# 514.自由之路

dp[i][j]表示第i步旋转至ring[j](==key[i])的最少操作步骤,状态转移方程为:
dp[i][j]=min{dp[i-1][k]+opt+1}(ring[k]==key[i-1], opt表示从ring[k]旋转至ring[j]的操作次数).

```cpp
class Solution {
public:
    int findRotateSteps(string ring, string key) {
        int len_key = key.size(), len_ring = ring.size();
        vector<vector<int>> dp(len_key, vector<int>(len_ring, INT_MAX));
        for(int i=0; i<len_ring; i++)
            if(ring[i] == key[0])
                dp[0][i] = min(i, len_ring - i) + 1;
        int min_opt = INT_MAX;
        for(int i=1; i<len_key; i++)
            for(int j=0; j<len_ring; j++){
                if(ring[j] != key[i])
                    continue;
                for(int k=0; k<len_ring; k++){
                    if(ring[k] != key[i-1])
                        continue;
                    int opt = INT_MAX;
                    if(j>k)
                        opt = min(j-k, len_ring+k-j);
                    else
                        opt = min(k-j, len_ring+j-k);
                    //cout<<dp[i-1][k]<<'\t'<<opt<<endl;
                    dp[i][j] = min(dp[i][j], dp[i-1][k] + opt + 1);
                }
            }
        for(int i=0; i<len_ring; i++)
            min_opt = min(min_opt, dp[len_key-1][i]);
        return min_opt;
    }
};
```

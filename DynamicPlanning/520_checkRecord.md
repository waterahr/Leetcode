# 520.学生出勤记录II

dp_l[i][j][k]表示第i天的出勤记录为'L'且有连续j+1个'L'且之前有k个'A'时的可奖励的记录,
dp_a[i]表示第i天的出勤记录为'A'时的可奖励的记录,
dp_p[i][j]表示第i天的出勤记录为'P'且之前有j个'A'时的可奖励的记录，状态转移方程为:
dp_l[i][0][0]=dp_p[i-1][0], 
dp_l[i][0][1]=dp_a[i-1]+dp_p[i-1][1], 
dp_l[i][1][0]=dp_l[i-1][0][0], 
dp_l[i][1][1]=dp_l[i-1][0][1], 
dp_a[i]=dp_l[i-1][0][0]+dp_l[i-1][1][0]+dp_p[i-1][0], 
dp_p[i][0]=dp_l[i-1][0][0]+dp_l[i-1][1][0]+dp_p[i-1][0], 
dp_p[i][1]=dp_l[i-1][0][1]+dp_l[i-1][1][1]+dp_a[i-1]+dp_p[i-1][1].

```cpp
class Solution {
public:
    int checkRecord(int n) {
        long MOD = 1000000007;
        vector<long> dp_a(n, 0);
        vector<vector<long>> dp_p(n, vector<long>(2, 0));
        vector<vector<vector<long>>> dp_l(n, vector<vector<long>>(2, vector<long>(2, 0)));
        dp_l[0][0][0] = 1;
        dp_a[0] = 1;
        dp_p[0][0] = 1;
        for(int i=1; i<n; i++){
            dp_l[i][0][0] = dp_p[i-1][0] % MOD;
            dp_l[i][0][1] = (dp_a[i-1] + dp_p[i-1][1]) % MOD;
            dp_l[i][1][0] = dp_l[i-1][0][0] % MOD;
            dp_l[i][1][1] = dp_l[i-1][0][1] % MOD;
            dp_a[i] = (dp_l[i-1][0][0] + dp_l[i-1][1][0] + dp_p[i-1][0]) % MOD;
            dp_p[i][0] = (dp_l[i-1][0][0]+dp_l[i-1][1][0]+dp_p[i-1][0]) % MOD;
            dp_p[i][1] = (dp_l[i-1][0][1]+dp_l[i-1][1][1]+dp_a[i-1]+dp_p[i-1][1]) % MOD;
        }
        int idx = n - 1;
        return (dp_l[idx][0][0] + dp_l[idx][0][1] + dp_l[idx][1][0] + dp_l[idx][1][1] + dp_a[idx] + dp_p[idx][0] + dp_p[idx][1]) % MOD;
    }
};
```

# 960.删列造序III

dp[i]表示以索引i结尾时满足条件的最长子序列的长度,状态转移方程为:dp[i]=max{dp[j]+1}(0<=j<i, check(A, i, j)).

```cpp
class Solution {
public:
    int minDeletionSize(vector<string>& A) {
        int len = A[0].length();
        vector<int> dp(len, 1);
        dp[0] = 1;
        int max_len = 1;
        for(int i=1; i<len; i++)
            for(int j=0; j<i; j++)
                if(check(A, i, j)){
                    dp[i] = max(dp[i], dp[j]+1);
                    max_len = max(max_len, dp[i]);
                }
        return len - max_len;
    }
    
private:
    bool check(vector<string>& A, int i, int j){
        for(string s:A)
            if(s[i] < s[j]) return false;
        return true;
    }
};
```

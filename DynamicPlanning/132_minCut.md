# 132.分割回文串II

dp_pal[i][j]表示字符串s[i:j+1]是否为回文串,状态转移方程为:dp_pal[i][j]=OR{dp_pal[i+1][j-1]&&s[i]==s[j]};
dp_cut[i]表示字符串s[:i+1]分割为回文子串的最小分割次数,dp_cut[i]=min{dp_cut[j]+1}(dp_pal[j+1][i]).

```cpp
class Solution {
public:
    int minCut(string s) {
        vector<vector<bool>> dp_pal(s.length(), vector<bool>(s.length(), false));
        for(int i=s.length()-1; i>=0; i--){
            dp_pal[i][i] = true;
            for(int j=i+1; j<s.length(); j++){
                dp_pal[i][j] = dp_pal[i][j] || ((j <= i+1 || dp_pal[i+1][j-1]) && s[i]==s[j]);
                //cout<<i<<' '<<j<<' '<<dp_pal[i][j]<<endl;
            }
        }
        vector<int> dp_cut(s.length(), INT_MAX);
        for(int i=0; i<s.length(); i++){
            if(dp_pal[0][i]){
                dp_cut[i] = 0;
                continue;
            }
            for(int j=0; j<i; j++)
                if(dp_pal[j+1][i])
                    dp_cut[i] = min(dp_cut[i], dp_cut[j] + 1);
        }
        return dp_cut.back();
    }
};
```

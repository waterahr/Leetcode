# 91.解码方法

dp[i]表示字符串string[:i+1]可能的解码方式个数,状态转移方程为:dp[i]=Sigma{dp[j]}(0<=j<i, string[j+1:i+1]可以解码成一个字符).

```cpp
class Solution {
public:
    int numDecodings(string s) {
        vector<int> dp(s.length(), 0);
        dp[0] = 1;
        if(s[0] == '0') return 0;
        for(int i=1; i<s.length(); i++)
            for(int j=i-2; j<i; j++)
                if(check(s.substr(j+1, i-j)))
                    dp[i] += j>=0?dp[j]:1;
        return dp.back();
    }
    
private:
    bool check(string s){
        if(s.length() == 1){
            return s != "0";
        }else if(s.length() == 2){
            int num = (s[0] - '0') * 10 + s[1] - '0';
            return num>=10 && num<=26;
        }else
            return false;
    }
};
```

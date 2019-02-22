# 467.环绕字符串中唯一的子字符串

dp[i]表示以字母表中的第i+1个字母结尾的子串中满足环绕字符串条件的最长字串数目.

```cpp
class Solution {
public:
    int findSubstringInWraproundString(string p) {
        int n = p.length();
        if(n==0) return 0;
        vector<int> dp(26, 0);
        int cur_max_len = 1;
        for(int i=0; i<n; i++){
            if(i>0 && (p[i]-p[i-1] == 1 || p[i-1]-p[i] == 25))
                cur_max_len++;
            else
                cur_max_len = 1;
            dp[p[i]-'a'] = max(dp[p[i]-'a'], cur_max_len);
        }
        int count = 0;
        for(int count:dp)
            count += temp;
        return count;
    }
};
```

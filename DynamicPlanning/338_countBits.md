# 338.比特位计数

dp[n]表示数字n的二进制中1的数目,递推关系式为dp[n]=dp[n>>1]+n%2.

```cpp
class Solution {
public:
    vector<int> countBits(int num) {
        vector<int> count(num+1);
        count[0] = 0;
        for(int i=1; i<=num; i++)
            count[i] = count[i>>1] + i%2;
        return count;
    }
};
```

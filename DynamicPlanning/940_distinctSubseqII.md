# 940.不同的子序列II

endsWith[i]来表示以第i个字母结束的子序列的数量,则新增的子序列源自于在前面的子序列结果后面添加现在的字母以及现在的字母单独构成的子序列,
状态转移方程为:endsWith[i]=sum(endsWith[:])+1.

```cpp
class Solution {
public:
    int distinctSubseqII(string S) {
        long endsWith[26] = {}, mod = 1e9 + 7;
        for (char c : S)
            endsWith[c - 'a'] = accumulate(begin(endsWith), end(endsWith), 1L) % mod;
        return accumulate(begin(endsWith), end(endsWith), 0L) % mod;
    }
};
```

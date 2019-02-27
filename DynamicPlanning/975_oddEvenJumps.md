# 975.奇偶跳

dp_odd[i]表示从索引i处开始寄跳时能否到达数组的末尾,dp_even[i]表示从索引i处开始开始偶跳时能否达到数组的末尾,状态转移方程为:
dp_odd[i]=dp_even[i->next],dp_even[i]=dp_odd[i->next].

```cpp
class Solution {
public:
    int oddEvenJumps(vector<int>& A) {
        int size = A.size();
        vector<pair<int, int>> next(size, {-1, -1});
        for(int i=0; i<size; i++){
            int odd = INT_MAX, even = INT_MIN;
            for(int j=i+1; j<size; j++){
                if(A[j] >= A[i] && A[j] < odd){
                    next[i].first = j;
                    odd = A[j];
                }
                if(A[j] <= A[i] && A[j] > even){
                    next[i].second = j;
                    even = A[j];
                }
            }
            //cout<<i<<' '<<next[i].first<<' '<<next[i].second<<endl;
        }
        vector<bool> dp_odd(size, false), dp_even(dp_odd);
        dp_odd[size-1] = true;
        dp_even[size-1] = true;
        int count = 1;
        for(int i=size-2; i>=0; i--){
            if(next[i].first != -1) dp_odd[i] = dp_even[next[i].first];
            if(next[i].second != -1) dp_even[i] = dp_odd[next[i].second];
            if(dp_odd[i])
                count++;
        }
        return count;
    }
};
```

果然还是超出时间限制了,主要是寻找下一跳的双重循环浪费了很多时间.

```cpp
class Solution {
public:
    int oddEvenJumps(vector<int>& A) {
        int size = A.size();
        vector<pair<bool, bool>> dp(size, {false, false});
        dp[size-1] = {true, true};
        map<int, int> value2index;
        value2index[A[size-1]] = size-1;
        int count = 1;
        for(int i=size-2; i>=0; i--){
            if(value2index.find(A[i]) != value2index.end()){
                dp[i].first = dp[value2index[A[i]]].second;
                if(dp[i].first) count++;
                dp[i].second = dp[value2index[A[i]]].first;
            }else{
                auto iter = value2index.lower_bound(A[i]);
                if(iter!=value2index.end()){
                    dp[i].first = dp[iter->second].second;
                    if(dp[i].first) count++;
                }
                iter = value2index.upper_bound(A[i]);
                if(iter!=value2index.begin()){
                    iter--;
                    dp[i].second = dp[iter->second].first;
                }
            }
            value2index[A[i]] = i;
        }
        return count;
    }
};
```

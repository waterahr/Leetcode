# 983.最低票价

dp[i]表示达到days[i]旅游时的最低票价,考察当前天days[i]与前一天days[i-1]可否买7、30天的通行证而达到省钱的目的.

```cpp
class Solution {
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {
        int min_cost = INT_MAX;
        dfs(days, costs, 0, min_cost);
        return min_cost;
    }
    
private:
    void dfs(vector<int>& days, vector<int>& costs, int cur_cost, int& min_cost){
        int len_days = days.size();
        if(len_days == 0){
            //cout<<cur_cost<<endl;
            min_cost = min(cur_cost, min_cost);
            return ;
        }
        for(int j=0; j<3; j++){
            if(cur_cost + costs[j] >= min_cost) continue;
            int cover_days = days[0];
            if(j == 1) cover_days = days[0] + 6;
            else if(j == 2) cover_days = days[0] + 29;
            vector<int> other_days;
            for(int k=1; k<len_days; k++)
                if(days[k] > cover_days) other_days.push_back(days[k]);
            dfs(other_days, costs, cur_cost+costs[j], min_cost);
        }
    }
};
```

超出时间限制...只能再想辙了！看了一下网上的解法,原来是最简单的动态规划思路,dp[i]表示第i天的最低消费,递推关系式为:
i∈days=>dp[i]=min(dp[i-1]+costs[0], dp[i-7]+costs[1], dp[i-30]+costs[2]);
!i∈days=>dp[i]=dp[i-1].

```cpp
class Solution {
public:
    int mincostTickets(vector<int>& days, vector<int>& costs) {
        unordered_set<int> travel(days.begin(), days.end());
        int dp[31] = {};
        for (int i=1; i<=days.back(); i++){
            if(travel.find(i) == travel.end()) dp[i%31] = dp[(i-1)%31];
            else dp[i%31] = min({dp[(i-1)%31] + costs[0],
            dp[max(0, i-7)%31] + costs[1], dp[max(0, i-30)%31] + costs[2]});
        }
        return dp[days.back()%31];
    }
};
```

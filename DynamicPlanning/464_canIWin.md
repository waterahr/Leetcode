# 464.我能赢吗

```cpp
class Solution {
public:
    bool canIWin(int maxChoosableInteger, int desiredTotal) {
        if(maxChoosableInteger * (maxChoosableInteger + 1) / 2 < desiredTotal) 
            return false;
        vector<char> state(maxChoosableInteger, '0');
        map<string, bool> m;
        return dfs(desiredTotal, state, m);
    }
    
private:
    bool dfs(int desiredTotal, vector<char> state, map<string, bool>& m){
        string cur = "";
        cur = accumulate(state.begin(), state.end(), cur);
        if(m.find(cur) != m.end()) return m[cur];
        for(int i=0; i<state.size(); i++)
            if(state[i] == '0'){
                state[i] = '1';
                if(desiredTotal <= i+1 || !dfs(desiredTotal - i - 1, state, m)){
                    m[cur] = true;
                    state[i] = '0';
                    return true;
                }
                state[i] = '0';
            }
        m[cur] = false;
        return false;
    }
};
```

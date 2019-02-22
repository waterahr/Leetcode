# 838.推多米诺

对于位置i处的多米诺牌,分别模拟其两侧的作用力,为了计算方便可以用-1表示左推、1表示右推,根据作用力的时间先后判断最终多米诺的朝向.

```cpp
class Solution {
public:
    string pushDominoes(string dominoes) {
        vector<int> ltor(dominoes.size()), rtol(dominoes.size());
        bool isPush = false;
        for(int i=0; i<dominoes.size(); i++){
            if(dominoes[i] == 'R'){
                isPush = true;
                ltor[i] = 1;
            }
            else if(dominoes[i] == 'L'){
                isPush = false;
            }
            else if(isPush){
                ltor[i] = ltor[i-1] + 1;
            }
        }
        isPush = false;
        for(int i=dominoes.size()-1; i>=0; i--){
            if(dominoes[i] == 'L'){
                isPush = true;
                rtol[i] = 1;
            }
            else if(dominoes[i] == 'R'){
                isPush = false;
            }
            else if(isPush){
                rtol[i] = rtol[i+1] + 1;
            }
        }
        string ans;
        for(int i=0; i<dominoes.size(); i++){
            if(ltor[i]==rtol[i]) ans+='.';
            else if(ltor[i] == 0 && rtol[i] != 0) ans += 'L';
            else if(ltor[i] != 0 && rtol[i] == 0) ans += 'R';
            else if(ltor[i] < rtol[i]) ans += 'R';
            else if(ltor[i] > rtol[i]) ans += 'L';
        }
        return ans;
    }
};
```

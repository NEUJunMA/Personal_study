# 40.combinationSum2 99.2
```CPP
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(),candidates.end());
        vector<vector<int>> res;
        vector<int> temp;
        combinationSumDFS(candidates,0,target,temp,res,0);
        sort(res.begin(),res.end());
        res.erase(unique(res.begin(), res.end()), res.end());
        return res;
    }
    void combinationSumDFS(vector<int>& candidates, int start, int target, vector<int>& temp, vector<vector<int>>& res, int flag){
        if(target<0)
            return;
        if(target==0){
            res.push_back(temp);
            return;
        }
        for(int i = start; i < candidates.size(); i++){
            if(target-candidates[i] < 0)
                break;            
            temp.push_back(candidates[i]);
            combinationSumDFS(candidates,i+1,target-candidates[i],temp,res,0);
            temp.pop_back();
        }
    }
};
```
# difference with 39:
* need to remove duplicate results because the input isn't a set
* need to use i+1 as next function start since we can't use this position again and again

# new Pruning alg
```cpp
class Solution {
public:
    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(),candidates.end());
        vector<vector<int>> res;
        vector<int> temp;
        combinationSumDFS2(candidates,0,target,temp,res);
        sort(res.begin(),res.end());
        res.erase(unique(res.begin(),res.end()),res.end());
        return res;
    }
    void combinationSumDFS2(vector<int>& candidates, int start, int target, vector<int>& temp, vector<vector<int>>& res){
        

           
        if(target<0)
            return;
        else if(target>0){
            for(int i = start; i < candidates.size();i++){
                if (i > start && candidates[i] == candidates[i - 1]) continue;
                if(target-candidates[i] < 0)
                    break;
                temp.push_back(candidates[i]);
                combinationSumDFS2(candidates,i+1,target-candidates[i],temp,res);
                temp.pop_back();
            }
        }
        else{
            res.push_back(temp);
            return;
        }
        
        
    }
};
```
* core: if (i > start && candidates[i] == candidates[i - 1]) continue;
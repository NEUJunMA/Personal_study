```cpp
class Solution {
public:
    int rob(vector<int>& nums) {
        if(nums.size()==0)
            return 0;
        if(nums.size()==1)
            return nums[0];
        vector<int> dp(nums.size(),0);
        dp[0]=nums[0];
        dp[1]=nums[1];
        for(int i=2;i<nums.size();i++){
            // cout<<dp[i-2]+nums[i]<<" "<<dp[i-1]-nums[i-1]+nums[i]<<endl;
            int temp=max(dp[i-2]+nums[i],dp[i-1]-nums[i-1]+nums[i]);
            dp[i]=max(temp,dp[i-1]);
            
        }
        return max(dp[nums.size()-1],dp[nums.size()-2]);
    }
};
```
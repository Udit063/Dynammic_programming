# House Robber Problem with Tabulation Approach

## Approach

Since, it a **bottom-up approach**, so, we will first declare a base case, for dp[0] and then traverse through the loop for the rest of the elements.

Now, we will also check for 'i=1', as because 'i-2' will go negative and hence, apply a condition for it.

## Code

```c++
    int rob(vector<int>& nums) {
        int n=nums.size();
        vector<int>dp(n,-1);
        dp[0]=nums[0];
        for(int i=1;i<n;i++){
            int pick = nums[i];
            if(i>1) pick += dp[i-2];
            int non_pick = 0 + dp[i-1];
            dp[i]=max( pick, non_pick);
        }
        return dp[n-1];
    }
```

**TC:** O(n)

**SC:** O(n)

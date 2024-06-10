# House Robber Problem with memoization problem

## Approach

Since, we have to find all the sequences of the houses and pick those that are not adjacent. Hence, we will perform recursion here to find all occurrences and modify it according to the problem.

Let's first pick the element of the last index, then according to the question we will add it and then pass to next to next element for non-adjency and get the sum for all and similarly if we do not have to pick that element then we move to the next element adding to 0.

For **Memoization**, declare the vector and store the sum in the indexes and check before picking and not picking.

## Code

```c++
    int f(vector<int>& nums, int ind, vector<int>& dp){
        if(ind==0) return nums[ind];
        if(ind<0) return 0;
        if(dp[ind] != -1) return dp[ind];
        int pick = nums[ind] + f(nums, ind-2, dp);
        int not_pick = 0 + f(nums, ind-1, dp);
        dp[ind] = max(pick, not_pick);
        return dp[ind];
    }

    int rob(vector<int>& nums) {
        int n=nums.size();
        vector<int>dp(n,-1);
        return f(nums, n-1, dp);
    }
```

**TC:** O(n)

**SC:** O(n)

# 0/1 knapsack Problem using Tabulation Approach

## Approach

For **tabulation(down -> up)**, just check for the **base cases** and make the **loop** for the changing variables, i.e., **ind & wt**, and then **copy the recursion** and modify it.

For base case, at **ind==0**, if **wt[i] <= w**, then **wt[i]** should return otherwise, return **0**.

## Code

```c++
    int findContentChildren(vector<int>& val, vector<int>& wt, int maxWt) {
        int n=val.size();
        vector<vector<int>> dp(n, vector<int> (maxWt+1, -1));

        for(int w=wt[0]; w<= maxWt; w++) dp[0][w]=val[0];

        for(int ind = 1; ind<n; ind++){
            for(int w=0; w<=maxWt; w++){
                int not_take = 0 + dp[ind-1][w];
                int take = INT_MIN;
                if(wt[ind] <= w) take = val[ind] + dp[ind-1][w-wt[ind]];
                dp[ind][w] = max(not_take, take)
            }
        }
        return dp[n-1][maxWt];
    }
```

**TC:** O(n\*w)

**SC:** O(n\*w)

# Frog Jump with k steps Through Memoization approach

## Approach

For (i+1), (i+2) ,....., (i+k) no. of steps, just circulate through the loop 'k' no of times, rest logic will be same for all.

## Code

```c++
    int f(int ind, int k, vector<int>& height, vector<int> &dp){
      if(ind==0) return 0;
      int minSteps=INT_MAX;
      if(dp[ind]!= -1) return dp[ind];
      for(int i=1;i<=k;i++){
        if(ind > (i-1)){
            int jump = f(ind-i, k , height,dp) + abs(height[ind]-height[ind-i]);
            minSteps = min(minSteps, jump);
            dp[ind]=minSteps;
        }
      }
      return dp[ind];
    }

    int minimizeCost(vector<int>& height, int n, int k) {
        vector<int> dp(n,-1);
        return f(n-1,k,height,dp);
    }

```

**TC:** O(n\*k)

**SC:** O(n)

# Frog Jump Question Through Memoization approach

## Approach

Since, we have to find the min of all cases, hence recursion will be applied.

1. Declare the vector and assigned with '-1'.
2. Add the base condition and also for the condition when index of vector is not equals to '-1'.
3. Move left and right and add the energies accordingly.
4. Store the result in the vector.

## Code

```c++
    int f(int ind, vector<int>& height, vector<int>& dp){
      if(ind == 0) return 0;

      if(dp[ind] != -1) return dp[ind];

      int left = f(ind-1, height,dp) + abs(height[ind] - height[ind-1]);
      int right  = INT_MAX;
      if(ind>1){
          right = f(ind-2, height,dp) + abs(height[ind] - height[ind-2]);
      }

      dp[ind]=min(left,right);
      return dp[ind];
  }

    int minimumEnergy(vector<int>& height, int n) {
        vector<int> dp(n,-1);
        return f(n-1, height, dp);
    }
```

**TC:** O(n)

**SC:** O(n)

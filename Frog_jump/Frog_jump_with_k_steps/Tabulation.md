# Frog Jump with k steps Through Tabulation approach

## Approach

Initialize the base conditon by declaring dp[0]=0;

Now for rest of the indexes, generate a loop and make a nested loop for the no of steps till k. Do the min operation and store it in the vector and return it.

## Code

```c++
    int minimizeCost(vector<int>& height, int n, int k) {
        vector<int> dp(n,-1);
        dp[0]=0;
        for(int i=1;i<n;i++){
            int minSteps = INT_MAX;
            for (int j=1;j<=k;j++){
                if(i > j-1){
                    int jump = dp[i-j] + abs(height[i]-height[i-j]);
                    minSteps = min(minSteps, jump);
                    dp[i]=minSteps;
                }
            }
        }
        return dp[n-1];
    }
```

**TC:** O(n\*k)

**SC:** O(n)

# Frog Jump with k steps Through Space Optimization approach

## Approach

First of all, no. of variables to be declared will be 'k' last values. Like for 2 steps, dp[i-1] and dp[i-2] will be required, whereas for 3 steps, dp[i-3] will also be required.

If (k==n), then in worst case, space occupied will be O(n). Hence, **It is not necessary for space optimization**

# Subset Sum Problem with Tabulation Approach

## Approach

For **tabluation (down - top)**, take the same dp array -> **dp[n][target]**.

Now declare the base cases.
Base cases:-

1. When **(target==0)**, then **i=(1,2,.....,n-1)**. So, **dp[i][0]=true**.
2. When **(ind == 0)**, then we check for arr[0], no matter what the target is. Hence, **dp[[0]a[0]]=true**.

Now, form the nested loops, **(1 -> n-1) for i** and **(1 -> sum) for target**.

At last, return **dp[n-1][sum]** what we had passed in recursion.

## Code

```c++
    bool isSubsetSum(vector<int>arr, int sum){
        int n=arr.size();
        vector<vector<bool>> dp(n,vector<bool>(sum+1, 0));

        for(int i=0; i<n; i++) dp[i][0] = true;
        dp[0][arr[0]] = true;

        for(int i=1; i<n; i++){
            for(int target=1; target <= sum; target++){
                int not_take = dp[i-1][target];
                bool take = false;
                if(target >= arr[i]) take = dp[i-1][target-arr[i]];
                dp[i][target] = not_take | take;
            }
        }

        return dp[n-1][sum];
    }
```

**TC:** O(n\*sum)

**SC:** O(n\*sum)

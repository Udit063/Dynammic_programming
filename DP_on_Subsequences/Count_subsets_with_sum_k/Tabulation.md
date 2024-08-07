# Count Subsets with Sum k Problem using Tabulation Approach

## Approach

For **tabulation (0-> n-1)**, first check for the **base cases**, then look at the changing paramenters and write **nested loop** and then copy the **recursion** and modify it.

We will take the same dp array, **dp[n][sum+1]**. For the base cases:-

1. When **(arr[0] == 0)**, then there are **2 cases**, either pick it or not pick it.
2. when **(ind == 0 && arr[0] != 0)**, **dp[0]a[0]] = 1**.

## Code

```c++
    int perfectSum(int arr[], int n, int sum)
	{
        vector<vector<int>> dp(n, vector<int>(sum+1, 0));
        if(arr[0] == 0) dp[0][0] = 2;
        else dp[0][0] = 1;

        // arr[0] = 0
        if(arr[0] != 0 && arr[0] <= sum) dp[0][arr[0]]=1;

        for(int ind = 1; ind < n; ind++){
            for(int target=0; target <= sum; target++){
                int not_pick = dp[ind-1][target];
	            int pick = 0;
	            if(arr[ind] <= target) pick = dp[ind-1][target - arr[ind]];
	            dp[ind][target] = pick + not_pick;
            }
        }
        return dp[n-1][sum];
	}
```

**TC:** O(n\*sum)

**SC:** O(n\*sum)

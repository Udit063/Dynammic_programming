#Partition with given difference Problem using Tabulation Approach

## Approach

Just same as the count subset problem with sum k and rest calculations as done in memoization.

## Code

```c++
    int perfectSum(vector<int>& arr, int n, int sum)
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
	            dp[ind][target] = (pick + not_pick) % mod;
            }
        }
        return dp[n-1][sum];
	}

    int countPartitions(int n, int d, vector<int>& arr) {
        int total_sum = 0;
        for(auto &it:arr) total_sum += it;
        if((total_sum - d) < 0 || (total_sum - d) % 2) return 0;
        return perfectSum(arr, n, ((total_sum - d) / 2));
    }
```

**TC:** O(n\*sum)

**SC:** O(n\*sum)

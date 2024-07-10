# Partition with given difference Problem using Memoization Approach

## Approach

We need to divide an array into two subsets with sum S1 and S2, such that, **S1 >= S2** and also **S1 - S2 = D**. So, we need to find totoal number of such pairs.

Now, we want, **S1 - S2 = D**

For S1, we can write as, **S1 = total_sum - S2**

Therefore, **(S2 = total_sum - D) / 2**

From this, we can conclude that, **(total_sum - D) >= 0** and also **(total_sum - D)** should be **even**, as S1 can't be in fraction. Also, we can see that, this is the same case as of **counting subsets with sum k**.

## Code

```c++
    int f(int ind, int sum, vector<int>& arr, vector<vector<int>>& dp){
	    if(ind==0) {
	        if(sum == 0 && arr[0] == 0) return 2;
	        if(sum == 0 || sum == arr[0]) return 1;
	        return 0;
	    }
	    if(dp[ind][sum] != -1) return dp[ind][sum];

	    int not_pick = f(ind-1, sum, arr, dp);
	    int pick = 0;
	    if(arr[ind] <= sum) pick = f(ind-1, sum - arr[ind], arr, dp);

	    return dp[ind][sum] = (pick + not_pick) % mod;
	}

	int perfectSum(vector<int>& arr, int n, int sum)
	{
        vector<vector<int>> dp(n, vector<int>(sum+1, -1));
        return f(n-1, sum, arr, dp);
	}

    int countPartitions(int n, int d, vector<int>& arr) {
        int total_sum = 0;
        for(auto &it:arr) total_sum += it;
        if(total_sum - d < 0 || (total_sum - d) % 2) return 0;
        return perfectSum(arr, n, ((total_sum - d) / 2));
    }
```

**TC:** O(n\*sum)

**SC:** O(n) + O(n\*sum)

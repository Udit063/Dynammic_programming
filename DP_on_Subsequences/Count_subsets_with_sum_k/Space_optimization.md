# Count Subsets with Sum k Problem using Space Optimization Approach

## Approach

Since, we can see in tabulation, we require **d[ind-1][]** and **dp[ind][]**, means the **prev** and **curr** row respectively. Hence, we can space optimize it using 2 **1D arrays**, prev and curr and make sure that for both the first value should be true at index 0 as we have declared in tabulation to fill all.

For the base case, we can see that **index 0** of every row is **1** in tabulation, so we will make our first element as 1.

## Code

```c++
    int perfectSum(int arr[], int n, int sum)
	{
        vector<int> prev(sum+1, 0), curr(sum+1, 0);
        prev[0] = curr[0] = 1;
        if(arr[0] <= sum) prev[arr[0]]=1;

        for(int ind = 1; ind < n; ind++){
            for(int target=0; target <= sum; target++){
                int not_pick = prev[target];
	            int pick = 0;
	            if(arr[ind] <= target) pick = prev[target - arr[ind]];
	            curr[target] = pick + not_pick;
            }
            prev = curr;
        }
        return prev[sum];
	}

```

**TC:** O(n\*sum)

**SC:** O(sum)

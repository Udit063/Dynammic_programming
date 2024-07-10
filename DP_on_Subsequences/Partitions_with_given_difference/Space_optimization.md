# Count Subsets with Sum k Problem using Space Optimization Approach

## Approach

Just same as the count subset problem with sum k and rest calculations as done in memoization.

## Code

```c++
    int perfectSum(int arr[], int n, int sum)
	{
        vector<int> prev(sum+1, 0), curr(sum+1, 0);
        if(arr[0] == 0) prev[0] = 2;
        else prev[0] = 1;

        // arr[0] = 0
        if(arr[0] != 0 && arr[0] <= sum) prev[arr[0]]=1;

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

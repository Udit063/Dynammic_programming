# Count Subsets with Sum k Problem using Memoization Approach

## Approach

Since, we need to find all possible ways or all the subsets whose **sum=k**, so, we will perform **recursion**. For counting in recursion, if **base case satisfies** then always **return 1** and if not then **return 0**. Now, after expressing in terms of index, explore all the possibilities, either **pick** the element or **not_pick**. After that, sum up all the possibilities, i.e., **pick + not_pick**.

It will give problem for the cases like **{0, 0, 1}** where ans should be **4** but it will give only **1**, so we need to go deeper and check for all the edge cases.

1. If at **ind = 0**, **arr[0] == 0**, and **sum == 0**, so we will have **2 cases**, either to pick it or to not pick it.
2. If at **ind = 0**, **arr[0] == 5**, and **sum == 5**, so we should take it in order to make **sum = 0**
3. If at **ind = 0**, **arr[0] == 5**, and **sum == 0**, so we can't take it as **arr[0] > sum**

## Code

```c++
    int f(int ind, int sum, int arr[], vector<vector<int>>& dp){
	    if(ind==0) {
	        if(sum == 0 && arr[0] == 0) return 2;
	        if(sum == 0 || sum == arr[0]) return 1;
	        return 0;
	    }

	    if(dp[ind][sum] != -1) return dp[ind][sum];

	    int not_pick = f(ind-1, sum, arr, dp);
	    int pick = 0;
	    if(arr[ind] <= sum) pick = f(ind-1, sum - arr[ind], arr, dp);

	    return dp[ind][sum] = pick + not_pick;
	}

	int perfectSum(int arr[], int n, int sum)
	{
        vector<vector<int>> dp(n, vector<int>(sum+1, -1));
        return f(n-1, sum, arr, dp);
	}
```

**TC:** O(n\*sum)

**SC:** O(n) + O(n\*sum)

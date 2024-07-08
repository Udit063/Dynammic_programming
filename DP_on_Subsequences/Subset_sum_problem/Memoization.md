# Subset Sum Problem with Memoization Approach

## Approach

For, checking any subsequence whose sum is equal to the target, we need to find all the subsequences and hence, do the recursion. If we found any ! subsequence whose sum = target, we can return true.

For recursion, we will take 2 arguments, ind and target(sum). For finding subsequences, we will either **take** that element or **don't take** that element. But before taking the element we have to check, if it is smaller than the target or not, and if it is greater then no need to take it as it won't be possible.

When you take the element then reduce the target and subtract that element from the target to find the rest from inner subsequences.

For **memoization**, we will be required for a **2D array -> dp[n][target]** and check before taking or not taking the element and storing the result in the end.

## Code

```c++
    bool f(int ind, int target, vector<int>arr, vector<vector<int>>&dp){
        if(target == 0) return true;
        if(ind == 0) return arr[0]==target;

        if(dp[ind][target] != -1) return dp[ind][target];

        bool not_take = f(ind-1, target, arr, dp);
        bool take = false;
        if(target >= arr[ind]) take = f(ind-1, target-arr[ind], arr, dp);

        return (dp[ind][target] = (not_take | take));
    }

    bool isSubsetSum(vector<int>arr, int sum){
        int n=arr.size();
        vector<vector<int>> dp(n,vector<int>(sum+1,-1));
        return f(n-1, sum, arr, dp);
    }
```

**TC:** O(n\*sum)

**SC:** O(n) + O(n\*sum)

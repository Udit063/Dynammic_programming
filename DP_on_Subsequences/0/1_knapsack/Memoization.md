# 0/1 knapsack Problem using Memoization Approach

## Approach

We are given a **weight of bag**, an **array of weight** and their **corresponding values**. We need to steal **max weight** in the bag out of the array.

Here, we cannot use greedy, as it will take the valuable first, so our max may be compromise. For ex, if our **bag=6**, array of weight with corresponding weight are :- **{(3, 30), (2, 40), (5, 60)}**. So, acc to greedy it will take **weight=5 first** and rest will left, but our **max value = 70 ( wt 2+3)**. So, we will have to find all ways, hence use **recursion**.

For recursion, we have to express in terms of **(ind, weight)**. Then, we have to explore all the possibilities by **taking** it or **not taking** it and then at last find the **maximum**.

For base case, **when(ind == 0), if(wt[0] <= w)**, then only return or take the value or else return 0.

## Code

```c++
    int f(int ind, int w, vector<int>& val, vector<int>& wt, vector<vector<int>>& dp){
        if(ind == 0){
            if(wt[0] <= w) return val[0];
            else return 0;
        }
        if(dp[ind][w] != -1) return dp[ind][w];
        int not_take = 0 + f(ind-1, w, val, wt);
        int take = INT_MIN;
        if(wt[ind] <= w) take = val[ind] + f(ind-1, w-wt[ind], val, swt;

        return dp[ind][w] = max(not_take, take);

    }

    // g -> values and s -> weight
    int findContentChildren(vector<int>& g, vector<int>& s, int maxWt) {
        int n=g.size();
        vector<vector<int>> dp(, vector<int> (maxWt+1, -1));
        return f(n-1, maxWt, g, s, dp);
    }
```

**TC:** O(n\*w)

**SC:** O(n) + O(n\*w)

# Rod cutting Problem using Memoization Approach

## Approach

In this question, we need to cut the rod in such a way that the **sum of part lengths** should be **equal** to the **total length** and the **price** corresponding to each length should be **maximize**. Since, we need to find all the possible lengths, hence, we will use **recursion**.

For recursion:-

1. Express in terms of **(index, N)**
2. Explore all possible ways **(take or not_take)**
3. return the **max** of both

For base case, for ex, when **rod length = 1**, if **N=12** and with **price = 6**. Then, total **12 rods of length 1 will be needed**. Hence, **N\*price[0]** will get returned.

For memoization, take a **dp[n][n+1] array** and store the result in it and always check before picking or not picking it.

## Code

```c++
    int f(int ind, int n, int price[], vector<vector<int>>& dp){
        if(ind == 0) return (n*price[0]);
        if(dp[ind][n] != -1) return dp[ind][n];
        int not_take = 0 + f(ind-1, n, price, dp);
        int take = INT_MIN;
        int rodLength = ind+1;
        if(rodLength <= n) take = price[ind] + f(ind, n-rodLength, price, dp);

        return dp[ind][n] = max(take, not_take);
    }

    int cutRod(int price[], int n) {
        vector<vector<int>> dp(n, vector<int>(n+1 , -1));
        return f(n-1, n, price, dp);
    }
```

**TC:** O(n\*n)

**SC:** O(n) + O(n\*n)

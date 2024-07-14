# Ways to make coin change Problem using Memoization Approach

## Approach

In this question, we need to find **total no of ways** such that coins can be added such that their **sum == amount** given. Repetition of coins is allowed.

Since, we need to find all the ways, hence, we will do **recursion**.

For recursion:-

1. Express in terms of **(index, amount)**
2. Explore all possible ways **(take or not_take)**
3. return the **sum** of both

For base case: base case will be at **(ind == 0)**. Suppose, **amount = 4** and **a[0] = 2 or 4**, then it will be possible **{2, 2}** or **{4}**. Hence, **if(amount % a[0] == 2) return 1, else 0.**

For memoization, make a dp array of **[N]\*[amount+1]** and store the ans in it. Also, before taking or not taking, check if it exists or not.

## Code

```c++
    int f(int ind, int amount, vector<int>& coins, vector<vector<int>>& dp){
        if(ind == 0){
            if(amount % coins[ind] == 0) return 1;
            else return 0;
        }
        if(dp[ind][amount] != -1) return dp[ind][amount];
        int not_take = f(ind-1, amount, coins, dp);
        int take = 0;
        if(coins[ind] <= amount) take = f(ind, amount - coins[ind], coins, dp);

        return dp[ind][amount] = (not_take + take);
    }

    int change(int amount, vector<int>& coins) {
        int n = coins.size();
        vector<vector<int>> dp(n, vector<int>(amount+1, -1));
        return f(n-1, amount, coins, dp);
    }
```

**TC:** O(n\*amount)

**SC:** O(amount) + O(n\*amount)

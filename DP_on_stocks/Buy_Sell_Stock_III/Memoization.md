# Buy and Sell Stock III using Memoization Approach

## Approach

In this question, we are given a **price array** and we have to first **buy** the stock then **sell** it such that the **profit is maximum**. But, the condition is, we can **buy & sell only 2 times** but in order to buy another, we have to sell the one before.

Since, at each step we have lot of options either to **buy it** or **sell it** or do **nothing** with it, so we will have a lot of ways, hence we have to **try all ways**, hence use **recursion**.

For recursion:-

1. Express in terms of **(index, buy, cap)**. **Buy = 1** means we can **buy it** and **buy = 0** means we cannot buy it, we have to **sell it**. **cap = 2**, will denote **total number of transactions**.
2. Explore all possible ways on that day like **(buy or not_buy)** or **(sell or not_sell)**
3. return the **max** of all profit made

If we **buy** a stock then -**price[i]** will be **added** and if we **sell** stock then **price[i]** will be **added**, as we have to **subtract** the **stock price bought** from the **stock price sold**.

For **base case**, whenever the array ends, means we have nothing left, neither buy nor sell, hence **return 0**. Also, **if(cap == 0)**, means we had done 2 transactions, hence **return 0**.

Since, it will create an **overlapping subproblem**, hence, we will use **memoization**.

For memoization, just take a **dp[n][2][3]** array and store the result in this array. Also, check if any value exists in this array before moving forward.

### Extra

This can also be done using **dp[n][4]**, where **4 = no of transactions**. Since, total **limitations = 2**, so, it will be **B S B S**, _(B -> buy & S -> sell)_. Hence, if **transaction is even**, it is the case of **buy** and if it is **odd**, then it will be the case of **sell**. So, we will not have to take a variable for buy or not.

## Code

```c++
    int f(int ind, int buy, int cap, int n, vector<int>& prices, vector<vector<vector<int>>>& dp){
        if(cap == 0) return 0;
        if(ind == n) return 0;

        if(dp[ind][buy][cap] != -1) return dp[ind][buy][cap];

        int profit = 0;
        if(buy) profit = max(-prices[ind] + f(ind+1, 0, cap, n, prices, dp), 0 + f(ind+1, 1, cap, n, prices, dp));
        else profit = max(prices[ind] + f(ind+1, 1, cap-1, n, prices, dp), 0 + f(ind+1, 0, cap, n, prices, dp));

        return dp[ind][buy][cap] = profit;
    }

    int maxProfit(vector<int>& prices) {
        int n = prices.size();
        vector<vector<vector<int>>> dp(n, vector<vector<int>>(2, vector<int>(3, -1)));
        return f(0, 1, 2, n, prices, dp);
    }
```

**TC:** O(n\*2\*3)

**SC:** O(n\*2\*3) + O(n)

# Best Time to Buy and Sell Stock I

## Approach

In this question, we are given a **price array** and we have to first **buy** the stock then **sell** it such that the **profit is maximum**.

For any **ith** element, **maximum profit** will be when, when we take the **minimum from its left**.

## Code

```c++
    int maxProfit(vector<int>& prices) {
    int mini = prices[0];
    int profit = 0;

    for(int i=1; i<prices.size(); i++){
        int cost = prices[i] - mini;
        profit = max(profit, cost);
        mini = min(mini, prices[i]);
    }
    return profit;
    }
```

**TC:** O(n)

**SC:** O(1)

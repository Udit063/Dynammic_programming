# Buy and Sell Stock II using Space Optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **ahead** and **curr** and change accourdingly.

<!-- optional -->

Instead of this, we can also use **4 different variables**, i.e., **ahead_NotBuy**, **ahead_Buy**, **curr_NotBuy** and **curr_Buy**. When, **buy = 0**, it is **notBuy** and when **buy = 1**, it is **buy**. At last, change for, **ahead_NotBuy = curr_NotBuy** and **ahead_Buy = curr_Buy**

## Code

```c++
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        vector<int> ahead(2, 0), curr(2, 0);
        ahead[0] = ahead[1] = 0;

        for(int ind = n-1; ind>=0; ind--){
            for(int buy=0; buy<2; buy++){
                int profit = 0;
                if(buy) profit = max(-prices[ind] + ahead[0], 0 + ahead[1]);
                else profit = max(prices[ind] + ahead[1], 0 + ahead[0]);
                curr[buy] = profit;
            }
            ahead = curr;
        }
        return ahead[1];
    }
```

**TC:** O(n\*2)

**SC:** O(2)

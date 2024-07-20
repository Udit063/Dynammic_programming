# Buy and Sell Stock III using using Space Optimization Approach

## Approach

For space optimization, convert the dp **3D array** into **2 - 2D arrays**, **ahead** and **curr** and change accourdingly.

## Code

```c++
    int maxProfit(vector<int>& prices) {
        int n = prices.size();

        vector<vector<int>> ahead(2, vector<int>(3, 0));
        vector<vector<int>> curr(2, vector<int>(3, 0));

        // base case is not needed as it is already 0
        for(int ind=n-1; ind>=0; ind--){
            for(int buy=0; buy<=1; buy++){
                for(int cap=1; cap<=2; cap++){
                    int profit = 0;
                    if(buy) profit = max(-prices[ind] + ahead[0][cap], 0 + ahead[1][cap]);
                    else profit = max(prices[ind] + ahead[1][cap-1], 0 + ahead[0][cap]);

                    curr[buy][cap] = profit;
                }
            }
            ahead = curr;
        }
        return ahead[1][2];
    }
```

**TC:** O(n\*2\*3)

**SC:** O(2\*3)

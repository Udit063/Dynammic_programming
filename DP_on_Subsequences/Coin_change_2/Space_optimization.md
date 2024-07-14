# Ways to make coin change Problem using Space optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **prev** and **curr** and change accourdingly.

## Code

```c++
    int change(int amount, vector<int>& coins) {
        int n = coins.size();

        vector<int> prev(amount+1, 0), curr(amount+1, 0);
        for(int i=0;i<=amount; i++) prev[i] = (i % coins[0] == 0);

        for(int ind=1; ind<n; ind++){
            for(int j=0; j<=amount; j++){
                int not_take = prev[j];
                int take = 0;
                if(coins[ind] <= j) take = curr[j - coins[ind]];
                curr[j] = (not_take + take);
            }
            prev = curr;
        }
        return prev[amount];
    }
```

**TC:** O(n\*amount)

**SC:** O(amount)

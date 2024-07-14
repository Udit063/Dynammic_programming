# Rod cutting Problem using Space optimization Approach

## Approach

For space optimization, convert the dp **2D array** into **2 1D arrays**, **prev** and **curr** and change accourdingly.

## Code

```c++
    int cutRod(int price[], int n) {
        vector<int> prev(n+1 , 0), curr(n+1, 0);
        for(int i=0; i<=n; i++) prev[i] = i*price[0];

        for(int ind=1;ind<n;ind++){
            for(int j=0; j<=n;j++){
                int not_take = 0 + prev[j];
                int take = INT_MIN;
                int rodLength = ind+1;
                if(rodLength <= j) take = price[ind] + curr[j-rodLength];

                curr[j] = max(take, not_take);
            }
            prev = curr;
        }
        return prev[n];
    }
```

**TC:** O(n\*n)

**SC:** O(n)

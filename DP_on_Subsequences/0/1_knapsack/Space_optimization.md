# 0/1 knapsack Problem using Space optimization Approach

## Approach

For **tabulation(down -> up)**, just check for the **base cases** and make the **loop** for the changing variables, i.e., **ind & wt**, and then **copy the recursion** and modify it.

For base case, at **ind==0**, if **wt[i] <= w**, then **wt[i]** should return otherwise, return **0**.

## Code

```c++
    int findContentChildren(vector<int>& val, vector<int>& wt, int maxWt) {
        int n=g.size();
        vector<int> prev(maxWt+1, 0), curr(maxWt+1, 0);

        for(int w=wt[0]; w<= maxWt; w++) prev[w]=val[0];

        for(int ind = 1; ind<n; ind++){
            for(int w=0; w<=maxWt; w++){
                int not_take = 0 + prev[w];
                int take = INT_MIN;
                if(wt[ind] <= w) take = val[ind] + prev[w-wt[ind]];
                curr[w] = max(not_take, take)
            }
        }
        return prev[maxWt];
    }
```

**TC:** O(n\*w)

**SC:** O(w)

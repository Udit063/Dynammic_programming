# Ninja's Training Problem with Memoization Approach

## Approach

Here, we cannot use greedy because it will go day wise and give the max point of each single day irrespective of what next same training offers. For ex, if on day 1 points are [5,2,1] and on day 2 [10,1,1], then it will give points **6 (5+1)** but our answer should be **12 (10 + 2)**.

So, we have to find all the occurences and return the maximum.

Hence, we will use **recursion**, and we will go through each days for all the training (0 -> 2). We will check for the points for each day and return the maximum.

## Code

```c++
    int f(int ind, int last, vector<vector<int>>& points, vector<vector<int>>& dp){
      if(ind == 0){
          int maxi=0;
          for(int i=0;i<3;i++){
              if(i != last){
                  maxi = max(maxi, points[ind][i]);
              }
          }
          return maxi;
      }

      if(dp[ind][last] != -1) return dp[ind][last];

      int maxi=0;
      for(int i=0;i<3;i++){
          if(i != last){
              int p = points[ind][i] + f(ind-1, i, points, dp);
              maxi = max(maxi, p);
          }
      }
      dp[ind][last] = maxi;
      return maxi;
  }

    int maximumPoints(vector<vector<int>>& points, int n) {
        vector<vector<int>> dp(n, vector<int>(4, -1));
        return f(n-1, 3, points , dp);
    }
```

**TC:** O((n*4)*3)

**SC:** O(n) + O(n\*4)

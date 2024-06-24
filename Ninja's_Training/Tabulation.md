# Ninja's Training Problem with Memoization Approach

## Approach

For tabulation (down-top), we will first declare the dp array as in memoization. Now, declare the base conditions for the day=0. Now, copy the same code as memoization and change for the array instead of calling for recursion.

## Code

```c++
    int maximumPoints(vector<vector<int>>& points, int n) {
        vector<vector<int>> dp(n, vector<int>(4, -1));

        dp[0][0] = max(points[0][1], points[0][2]);
        dp[0][1] = max(points[0][0], points[0][2]);
        dp[0][2] = max(points[0][0], points[0][1]);
        dp[0][3] = max(points[0][0], max(points[0][1], points[0][2]));

        for(int day=1; day<n; day++){
            for(int last=0; last < 4; last++){
                dp[day][last]=0;

                for(int task=0; task<3; task++){
                    if(task != last){
                        int p = points[day][task] + dp[day-1][task];
                        dp[day][last] = max(dp[day][last], p);
                    }
                }
            }
        }
        return dp[n-1][3];
    }
```

**TC:** O((n*4)*3)

**SC:** O(n) + O(n\*4)

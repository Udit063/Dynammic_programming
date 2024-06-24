# Unique path find Problem in 2D with Tabulation Approach

## Approach

If there is prev row & prev col, we can optimize it.
Since, it is **dp[i][j]=dp[i-1][j] + dp[i][j-1]**, hence, we can see that, we only require the previous element and the previous row.
So, we will declare two arrays, one denoting the previous array while other will be denoting current array and we will update the prev to curr on each next row.

## Code

```c++
    int uniquePaths(int m, int n) {
        vector<int> prev(n,0);

        for(int i=0;i<m;i++){
            vector<int> curr(n,0);
            for(int j=0;j<n;j++){
                if(i==0 && j==0){
                    curr[j]=1;
                }
                else{
                    int up=0, left=0;
                    if(i>0) up=prev[j];
                    if(j>0) left=curr[j-1];
                    curr[j]=up+left;
                }
            }
            prev=curr;
        }
        return prev[n-1];
    }
```

**TC:** O(m\*n)

**SC:** O(n)

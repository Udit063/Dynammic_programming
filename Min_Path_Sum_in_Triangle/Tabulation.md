# Minimum path Sum Problem in Triangle with Tabulation Approach

## Approach

Since, we require the **current row** and the **next row** for performing the operation. Hence, declare 2 arrays, 1 for current and 1 for the prev or front array and perform the operations accordingly.

## Code

```c++
    int minimumTotal(vector<vector<int>>& triangle) {
        int n=triangle.size();

        vector<int> prev(n,0);

        for(int j=0;j<n;j++) prev[j] = triangle[n-1][j]; //Base case

        for(int i=n-2;i>=0;i--){
            vector<int> curr(n,0);
            for(int j=i;j>=0;j--){
                int down = triangle[i][j] + prev[j];
                int diag = triangle[i][j] + prev[j+1];
                curr[j] = min(down, diag);
            }
            prev=curr;
        }
        return prev[0];
    }
```

**TC:** O(n\*n)

**SC:** O(n)

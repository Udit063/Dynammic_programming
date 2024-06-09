# Frog Jump Question Through Memoization approach

## Approach (Bottom-Up)

Intialize the base condition and implement the loop till the last.

Check for left and right condition and store the operation performed it in the vector.

## Code

```C++
    int minimumEnergy(vector<int>& height, int n) {
        vector<int> dp(n,0);
        dp[0]=0;
        for(int i=1;i<n;i++){
            int l=dp[i-1]+abs(height[i]-height[i-1]);
            int r=INT_MAX;
            if(i>1){
                r=dp[i-2]+abs(height[i]-height[i-2]);
            }
            dp[i]=min(l,r);
        }
        return dp[n-1];
    }
```

**TC:** O(n)

**SC:** O(n)

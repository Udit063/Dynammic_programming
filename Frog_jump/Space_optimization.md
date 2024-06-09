# Frog Jump Question Through Space Optimization approach

## Approach

Just remove the assigned vector and declare the variables prev2, prev and curr.

Now, as we move forward:

- curr = min (left , right)
- prev2 = prev
- prev = curr

## Code

```C++
    int minimumEnergy(vector<int>& height, int n) {
        int prev2=0;
        int prev=0;
        int curr;
        for(int i=1;i<n;i++){
            int l = prev + abs(height[i]-height[i-1]);
            int r = INT_MAX;
            if(i > 1){
                r = prev2 + abs(height[i]-height[i-2]);
            }
            curr=min(l , r);
            prev2=prev;
            prev=curr;
        }
        return curr;
    }
```

**TC:** O(n)

**SC:** O(1)

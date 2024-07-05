# Subset Sum Problem with Space Optimization Approach

## Approach

Since, we can see in tabulation, we require **d[ind-1][]** and **dp[ind][]**, means the **prev** and **curr** row respectively. Hence, we can space optimize it using 2 **1D arrays**, prev and curr and make sure that for both the first value should be true at index 0 as we have declared in tabulation to fill all.

## Code

```c++
   bool isSubsetSum(vector<int>arr, int sum){
        int n=arr.size();
        vector<bool> prev(sum+1, 0), curr(sum+1, 0);

        prev[0] = curr[0] = true;
        if(arr[0] <= sum) prev[arr[0]]=true;

        for(int i=1; i<n; i++){
            for(int target=1; target <= sum; target++){
                int not_take = prev[target];
                bool take = false;
                if(target >= arr[i]) take = prev[target-arr[i]];
                curr[target] = not_take | take;
            }
            prev=curr;
        }

        return prev[sum];
    }
```

**TC:** O(n\*sum)

**SC:** O(sum)

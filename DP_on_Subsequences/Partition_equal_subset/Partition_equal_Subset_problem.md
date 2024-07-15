# Partition Equal Subset Sum Problem with Space Optimization Approach

## Approach

We need to divide the array into 2 parts such that their sum should be equal. So, we can conclude that if an array has sum **a = S**, then it should be divided into 2 parts such that **a1 = a2 = S/2**.

So, if we found any subset whose **sum = S/2**, the sum of other subset will also be equal to **S/2 from this, S - S/2**. But, if the sum of array is **odd**, then S/2 will not be possible, hence will return **false**. Hence, it is same as of the **subset sum problem**, just the sum will be **S/2**.

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

    bool canPartition(vector<int>& nums) {
        int total_sum = 0;
        for(int i=0;i<nums.size();i++) total_sum += nums[i];

        if(total_sum % 2) return false;
        int sum = total_sum/2;
        return isSubsetSum(nums, sum);
    }
```

**TC:** O(n\*sum) + O(n)

**SC:** O(sum)

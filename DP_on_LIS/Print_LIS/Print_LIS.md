# Print LIS using Tabulation Approach

## Approach

Just that we had done in the **Tabulation_optimal** solution, that we had taken the **dp array storing length of LIS**. Now, we will take 1 more **hash array** which will **store the previous element from which ith element had been updated from**. Let's take an example, **a[] = [5, 4, 11, 1, 16, 8]** and **dp[i]** will be storing the **length of LIS till ith index**, i.e., **dp[n] = [1, 1, 2, 1, 3, 2]** now we will take one more **hash array** which will get **updated** whenever **dp array gets updated** and hash table will be **hash[n] = [0, 1, 0, 3, 2, 0]**, hence we can see that **max length of LIS is at ind = 4** from **dp array**, and **according to hash table** we will go from **ind = 4 to ind = 2 and then to ind = 0** and output will be **{16, 11, 5}**. Hence, store the output in an array and **reverse** the array.

## Code

```c++
    vector<int> longestIncreasingSubsequence(int n, vector<int>& nums) {
        vector<int> dp(n, 1), hash(n);
        int maxi = 1;
        int lastIndex = 0;

        for(int ind=0; ind<n; ind++){
            hash[ind] = ind;
            for(int prev_ind = 0; prev_ind < ind; prev_ind++){
                if(nums[ind] > nums[prev_ind] && 1+dp[prev_ind] >  dp[ind]) {
                    dp[ind] = 1 + dp[prev_ind];
                    hash[ind] = prev_ind;
                }
            }

            if(dp[ind] > maxi){
                maxi = dp[ind];
                lastIndex = ind;
            }
        }
        vector<int> temp;
        temp.push_back(nums[lastIndex]);

        while(hash[lastIndex] != lastIndex){
            lastIndex = hash[lastIndex];
            temp.push_back(nums[lastIndex]);
        }

        reverse(temp.begin(), temp.end());

        return temp;
    }
```

**TC:** O(n\*n)

**SC:** O(n)

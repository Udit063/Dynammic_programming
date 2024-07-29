# Matrix Chain Multiplication using Memoization Approach

## Approach

**Partition DP** is different from different DP and it is required where **partitions are done**. For ex, if we have to **multiply N matrices**, like **ABCD**, then it can be multiplied in different ways like, **A(BCD)**, **(AB)(CD)**, **(ABC)D**, so where we have to find all ways in partition, we use **Partition DP**.

In this question, we need to find **min no of operations** to multiply N matrices.

For **matrix chain multiplication**, we will be given an array, for ex, **[10, 20, 30, 40, 50]**, so matrices will be, **A = 10 X 20**, **B = 20 X 30**, **C = 30 X 40** and **D = 40 X 50**, hence, **ith = A[i-1] X A[i]**. If we need to find **AB** then, **no of operations = 10 X 20 X 30**.

Rules for Partition DP:-

1. Start will entire block/ array **(i, j)**, where **i = starting point** and **j = ending point**
2. Try all partitions -> Run a loop to try all partitions **(no of partitions, k from i -> j)**
3. Return the best possible 2 partitions ((A)(BCD) or (AB)(CD))

For **base case**, when **(i==j)**, means there is only **single matrix** and hence it will return no multiplication, hence, **return 0**.

Now for partitions, Loop will run from **(k = i -> j-1)** and partitions will be done like, **f(i, k) + f(k+1, j)**, to divide into **different partitions**. We have taken **(j-1)** bcz when we call for **f(k+1, j)**, it will get **out of j**.

When we check for **no of operations**, then we can see that, **no of operations = A[i-1] X A[k] X A[j] + partitions**. For ex, for array, **[10, 20, 30, 40, 50]**, **i=1**, **k=2** and **j=4**. Now, **partitions = (AB)(CD)**. **AB = 10 X 30** and **CD = 30 X 50**, hence, **no of operations = 10 X 30 X 50**, i.e., **A[i-1] X A[k] X A[j]**

Now, after this step, return **min of all steps**.

## Code

```c++
    int f(int i, int j, int arr[], vector<vector<int>>& dp){
        if(i==j) return 0;
        int mini = 1e9;

        if(dp[i][j] != -1) return dp[i][j];

        for(int k=i; k<j; k++){
            int steps = (arr[i-1]*arr[k]*arr[j]) + f(i, k, arr, dp) + f(k+1, j, arr, dp);
            mini = min(mini, steps);
        }

        return dp[i][j] = mini;
    }

    int matrixMultiplication(int N, int arr[])
    {
        vector<vector<int>> dp(N, vector<int>(N, -1));
        return f(1, N-1, arr, dp);
    }
```

**TC:** O(n\*n)*n = O(n*n\*n)

**SC:** O(n\*n) + O(n)

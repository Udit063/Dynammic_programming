# Length of Longest Increasing Subsequence using Binary Search Approach

## Approach

Since in all previous methods, for best approach, **TC: O(n\*n)** and **SC: O(n)**, but if **N=10^5**, so time limit will get exceeded to **TC: O(10^10)**, which may give a **TLE**, hence, we will use **binary search** for more optimal solution.

Let's take an example, **[1, 7, 8, 4, 5, 6, -1, 9]**. Now, we can **store** the **greater element** than the last in the same array and if not then store it in another array, for ex, for this array, arrays can be form like, **[1, 7, 8, 9]**, **[1, 4, 5, 6, 9]** and **[-1, 9]**, and **max length = 5**.

But making subsequeces at every step takes up a **lot of space**, hence, we will **rewrite the element**, like after **[1, 7, 8]** when we take **4**, we will **replace 7 with 4** and then **8 with 5** and so on. Since, our objective is to find the length only, hence **array size** will give us the **max length**.

For searching element equal or greater than, we can use **lower_bound()** function that gives the **index of the element found** or the **index of first element greater than our element**. Or we can use **Binary search** for searching this type of index which is best suitable.

## Code

```c++
    int longestSubsequence(int n, int a[])
    {
       vector<int> temp;
       temp.push_back(a[0]);
       for(int i=1; i<n; i++){
           if(a[i] > temp.back()) temp.push_back(a[i]);
           else{
               int ind = lower_bound(temp.begin(), temp.end(), a[i]) - temp.begin();
               temp[ind] = a[i];
           }
       }
       return temp.size();
    }
```

**TC:** O(n\*log(n))

**SC:** O(n)

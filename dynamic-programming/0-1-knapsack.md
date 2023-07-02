---
layout:
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# 0/1 Knapsack

### Problem Statement

You are given weights and values of **N** items, put these items in a knapsack of capacity **W** to get the maximum total value in the knapsack. Note that we have only **one quantity of each item**.

In other words, given two integer arrays **val\[0..N-1]** and **wt\[0..N-1]** which represent values and weights associated with **N** items respectively. Also given an integer W which represents knapsack capacity, find out the maximum value subset of **val\[]** such that sum of the weights of this subset is smaller than or equal to **W.** You cannot break an item, **either pick the complete item or don't pick it (0-1 property)**.

**Example :**

<pre><code><strong>Input:
</strong>N = 3
W = 4
values[] = {1,2,3}
weight[] = {4,5,1}
<strong>Output: 3
</strong></code></pre>

**Identification :**&#x20;

* Choice : item can be included or not included
* Optimal : return maximum total value in the knapsack.

**Intuition:**

**Recursive Solution:**

```cpp
// W : weight of knapsack
// wt[] : weight array
// val[] : value array
// n : size of weight/value array

int knapSack(int W, int wt[], int val[], int n) 
{ 
   // Your code here
   if(n==0 || W==0){
       return 0;
   }
   
   // if weight of nth element is less than knapsack's weight : can be included or cannot be included both cases are covered below
   if(wt[n-1]<=W){
       return max(val[n-1]+knapSack(W-wt[n-1],wt,val,n-1),knapSack(W,wt,val,n-1));
   }else{
   // if weight of nth element is greater than knapsack's weight : cannot be included
       knapSack(W,wt,val,n-1);
   }
}
```

**Memoized Solution:**

```cpp
// W : weight of knapsack
// wt[] : weight array
// val[] : value array
// n : size of weight/value array

int dp[1002][1002] // according to constraints given
memset(dp,-1,sizeof(dp));

int knapSack(int W, int wt[], int val[], int n) 
{ 
   // Your code here
   if(n==0 || W==0){
       return 0;
   }
   
   if(dp[n][W] != -1) return dp[n][W];
   
   // if weight of nth element is less than knapsack's weight : can be included or cannot be included both cases are covered below
   if(wt[n-1]<=W){
       return dp[n][W] = max(val[n-1]+knapSack(W-wt[n-1],wt,val,n-1),knapSack(W,wt,val,n-1));
   }else{
   // if weight of nth element is greater than knapsack's weight : cannot be included
       dp[n][W] = knapSack(W,wt,val,n-1);
   }
}
```

**DP Top Down Solution:**

* Trying to emit the recursive calls so that stack does not run out of space.
* Every grid cell represents maximum profit with i elements taken and knapsack's total weight of j. These cells represent solutions to sub problems.
* Initialisation : When knapsack's weight (W/j) == 0 and 0 items are taken (i==0, n==0), then maximum profit is 0.
* Base condition in recursive solution can be changed to initialisation of matrix.
*

```cpp
// W : weight of knapsack
// wt[] : weight array
// val[] : value array
// n : size of weight/value array

int knapSack(int W, int wt[], int val[], int n) 
{  

    vector<vector<int>>dp(n+1,vector<int>(W+1,-1));
    
   // initialisation
   // if(n==0 || W==0) return 0; turns to :
   for(int i=0;i<dp.size();i++){
       for(int j=0;j<dp[0].size();j++){
           if(i==0 || j==0) dp[i][j]=0;
       }
   }
   
   for(int i=1;i<n+1;i++){
       for(int j=1;j<W+1;j++){
           // if weight of nth element is less than knapsack's weight : can be included or cannot be included both cases are covered below
           if(wt[i-1]<=j){
               dp[i][j] = max(val[i-1]+dp[i-1][j-wt[i-1]], dp[i-1][j]);
           }
            // if weight of nth element is greater than knapsack's weight : cannot be included
           else dp[i][j] = dp[i-1][j]
       }
   }
   
   return dp[n][W];
}
```

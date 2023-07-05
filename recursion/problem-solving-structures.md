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

# Problem Solving Structures

### Pick/Not Pick Model

Suppose there is a problem to print all subsequences of an array without modifying the order. The given array is : { 3, 1, 2 }. In this case this case following subsequences can be printed :&#x20;

<figure><img src="../.gitbook/assets/Screenshot 2023-07-04 at 6.34.10 PM.png" alt=""><figcaption></figcaption></figure>

During every iteration either the recursion can pick / not pick the arr\[idx] at that iteration.

For exp : \[3, 1, 2]\
Subsequence -> \[3, 2]\
3 - arr\[0] ->pick   1 - arr\[1] -> !pick   2 - arr\[2] -> pick

```cpp
void rec(vector<int>&arr, int idx, vector<int>&res){
    if(idx == arr.size()){
        for(auto it : res) cout<<it<<" ";
        cout<<endl;
        return;
    }
    // pick
    res.push_back(arr[idx]);
    rec(arr,idx+1,res);
    // not pick
    res.pop_back();
    rec(arr,idx+1,res);
}

int main() {
    // Write C++ code here
    vector<int>arr={3,1,2};
    for(auto it:arr) cout<<it<<" ";
    cout<<endl;
    cout<<"-- All subsequences --"<<endl;
    vector<int>res;
    
    rec(arr,0,res);

    return 0;
}
```

### Recursive Diagram

<figure><img src="../.gitbook/assets/WhatsApp Image 2023-07-05 at 8.53.31 AM.jpeg" alt=""><figcaption></figcaption></figure>

### Recursion Tree

<figure><img src="../.gitbook/assets/WhatsApp Image 2023-07-05 at 8.53.26 AM.jpeg" alt=""><figcaption></figcaption></figure>

### Complexity

For every index we have 2 options of picking and not picking. Therefore if size of array/string == n :&#x20;

Time Complexity : O(2^n \* N (for loop used for printing))

Space Complexity : O(N) (Auxillary Space)

### Print subsequences with sum K

1. Add a sum variable in rec function
2. Before. every pick and not pick recursion calls add and remove the arr\[idx] from the sum respectively.
3. In the base condition add an if statement saying if sum == k then print the subsequence.

```cpp
void rec(vector<int>&arr, int idx, vector<int>&res, int sum){
    if(idx == arr.size()){
        if(sum==2){
            for(auto it : res) cout<<it<<" ";
            cout<<endl;
        }
        return;
    }
    // pick
    res.push_back(arr[idx]);
    sum+=arr[idx];
    rec(arr,idx+1,res,sum);
    // not pick
    res.pop_back();
    sum-=arr[idx];
    rec(arr,idx+1,res,sum);
}
```

### Print only 1 subsequence with sum K

1. Make function boolean && return true in base condition
2. if a subsequence is found return true to avoid further recursion calls otherwise return false.

<pre class="language-cpp"><code class="lang-cpp"><strong>bool rec(vector&#x3C;int>&#x26;arr, int idx, vector&#x3C;int>&#x26;res, int sum){
</strong>    if(idx == arr.size()){
        if(sum==k){
            for(auto it : res) cout&#x3C;&#x3C;it&#x3C;&#x3C;" ";
            cout&#x3C;&#x3C;endl;
            return true;
        }
        return false;
    }
    
    // pick
    res.push_back(arr[idx]);
    sum+=arr[idx];
    if(rec(arr,idx+1,res,sum)) return true;
    // not pick
    res.pop_back();
    sum-=arr[idx];
    if(rec(arr,idx+1,res,sum)) return true;
    
    return false;
}
</code></pre>

### Print number of subsequences with sum K

```cpp
// COUNT ALL SUBSEQUENCES
int rec(vector<int>&arr, int idx){
    if(idx == arr.size()) return 1;
    
    // pick
    res.push_back(arr[idx]);
    int pick = rec(arr,idx+1,res);
    // not pick
    res.pop_back();
    int not_pick = rec(arr,idx+1,res);
    
    return pick + not_pick;
}

// COUNT ALL SUBSEQUENCES WITH SUM K
int rec(vector<int>&arr, int idx, vector<int>&res, int sum){
    if(idx == arr.size()){
        if(sum==k) return 1;
        else return 0;
    }
    
    // pick
    res.push_back(arr[idx]);
    sum+=arr[idx];
    int l = rec(arr,idx+1,res,sum)
    // not pick
    res.pop_back();
    sum-=arr[idx];
    int r = rec(arr,idx+1,res,sum)
    
    return l+r;
}
```

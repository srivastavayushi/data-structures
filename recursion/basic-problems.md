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

# Basic Problems

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

### &#x20;Recurssion Tree

<figure><img src="../.gitbook/assets/WhatsApp Image 2023-07-05 at 8.53.26 AM.jpeg" alt=""><figcaption></figcaption></figure>

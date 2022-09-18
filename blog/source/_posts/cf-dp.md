---
title: cf-dp
date: 2022-09-15 12:50:52
tags: [algorithm,dp]

---
## dp学习
### [A1. Burenka and Traditions (easy version)](https://codeforces.com/problemset/problem/1718/A1)
> 对边界信息敏感 快速贪心
1. 维护多个操作信息， 单纯的贪心只能维护一组信息(***如何想到dp***)
2. dp[i][j]代表前i-1个数字处理为0，且最后一个数字为j的**最少**方案数  
> dp一定要可以求出答案，在过程处理中记得考虑保留答案信息

<details>
   <summary>**code**</summary>
   
```c++

#include<bits/stdc++.h>
using namespace std;
 
typedef long long ll;
typedef pair<int,int>PII;
#define endl '\n'
#define io ios::sync_with_stdio(false),cin.tie(0)
const int INF = 0x3f3f3f3f;
 
int n,m,k,T;
 
 
const int N = 5e3+10;
int a[N];
int dp[N][8193];
 
void solve(){
    cin >> n;
    for (int i = 1;i<=n;++i) cin >> a[i];
 
    // 初始化
    // for (int i = 0;i<8192;++i)[
    //     dp[1][i]=1;
    // ]
    // dp[1][a[1]]=0;
 
 
    for (int i = 1;i<=n;++i){
        for (int j = 0;j<8192;++j){
            dp[i][j] = dp[i-1][0] + (j!=a[i]);
        }
        for (int j = 0;j<8192;++j){
            dp[i][j^a[i]] = min (dp[i-1][j]+1,dp[i][j^a[i]]);
        }
 
    }
 
    cout << dp[n][0]<<endl;
 
}
 
int main(){
    
    // freopen("input.txt","r",stdin);
    // freopen("output.txt","w",stdout);
    io;
    cin >> T;
    while (T--)
    solve();
    return 0;
}
```


</details>


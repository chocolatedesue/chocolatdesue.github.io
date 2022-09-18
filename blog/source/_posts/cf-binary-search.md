---
title: cf-binary_search with monotonicity
date: 2022-09-18 04:37:08
tags: [algorithm,bs,mono,two_index]
---

## 二分相关算法学习
### [C. Binary String](https://codeforces.ml/contest/1680/problem/C)
1. 边界看情况 开大开小或正好(out of boundary)
2. prefix 和 suffix 数组含义和操作(不能转换)

<details>
   <summary>**code**</summary>
   
```c++

#include<bits/stdc++.h>
using namespace std;
 
typedef long long ll;
typedef pair<ll,ll>PII;
#define endl '\n'
#define io ios::sync_with_stdio(false),cin.tie(0)
const ll INF = 0x3f3f3f3f;
 
ll n,m,k,T;
string s;
 
 
// void debug(){
//     for (ll i = )
// }
 
bool check(ll u,const vector<ll>&pre,const vector<ll>&suf,const ll& zeros){
    ll rm0 = 0;
    // const ll cnt1 = pre.size();
    for (ll i = 0;i<=u;++i){
        rm0 = max (rm0,pre[i]+suf[u-i]);
    }
 
    ll remain0 = zeros-rm0;
    // ll remain0 = pre[cnt1-1]-rm0;
    // cout << remain0<<"---"<<endl;
    return remain0<=u;
}
 
void solve(){
    
    cin >> s;
    // s=" "+s;
    const ll len = s.size();
    // vector<ll>pre(len+1),post(len+1);
    ll zeros = count(s.begin(),s.end(),'0');
    ll ones = count(s.begin(),s.end(),'1');
 
 
    vector<ll>pre,suf;
    // ll cnt1 = 0,cnt0=0;
    ll cnt = 0;
    for (ll i = 0;i<len;++i){
        if (s[i]=='0'){
            cnt++;
        }
        else pre.push_back(cnt);
    }
    pre.push_back(cnt);
 
    cnt = 0;
    for (ll i = len-1;~i;--i){
        if (s[i]=='0') cnt++;
        else suf.push_back(cnt);
    }
 
    suf.push_back(cnt);
 
 
    
   
    ll l = 0, r=ones,mid;
    while (l<r){
        mid = l+r>>1;
        // cout << l<<" "<<r<<" "<<mid<<endl;
        if (check(mid,pre,suf,zeros)){
            // l = mid;
            r = mid;
        }
        else l = mid+1;
        
    }
    cout << l<<endl;
 
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



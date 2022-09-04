---
title: 第一次训练赛 4h
date: 2022-09-03 11:58:08
tag: 
mathjax: true
---


> [题目](/download/practice.pdf)
1. 开题慢，卡壳，没有快速定位能做的题
2. 没有规定卡结束时间，最后冲刺决策没有训练
3. 分散的太开了，开题多没写出来
4. 分工不太熟悉  

## 补题
### D. Fill The Bag
> [链接](https://codeforces.com/contest/1303/problem/D)
> 读题，保证$a[i]=2^i$,即a[i]代表一位二进制位 想到用二进制拆分解题


坑点 
1. 借位的代码实现， 被借位要减1
2. qpow (base,idx) 提供的参数反了

```c++
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
typedef pair<ll,ll>PII;
#define endl '\n'
#define io ios::sync_with_stdio(false),cin.tie(0)
const ll INF = 0x3f3f3f3f;
const ll N = 1e5+10;
ll n,m,k,T;
ll f[N];
ll cnt[100];

ll qpow(ll base,ll x){
    ll res = 1;
    while (x){
        if (x&1) res*=base;
        base*=base;
        x>>=1;
    }
    return res;

}

void debug(vector<ll>ans){
    for (auto i : ans){
        cout << i<<" ";
    }
    cout << endl;
}

ll calc(){
    ll nums = 0;
    vector<ll>ans;
    ll tmp = m;
    while (tmp){
        if (tmp&1) ans.push_back(1);
        else ans.push_back(0);
        tmp>>=1;
        // cout <<"tmp "<<tmp<<endl;
    }
    // cout <<"--"<<m<<endl;
    // debug(ans);
    for (ll i = 0;i<ans.size();++i){
        if (!ans[i]){
            cnt[i+1]+=cnt[i]/2;
            continue;
        }
        if (cnt[i]){
            cnt[i]--;
            cnt[i+1]+=cnt[i]/2;
        }
        else {
            ll k = i+1;
            while (!cnt[k]){
                k++;
            }
            cnt[k]-=1;
            nums+=(k-i);
            cnt[i+1]+=qpow(2,(k-i-1))-1;
            // cout << cnt[3]<<"---"<<endl;
        }

    }
    return nums;

}

void add (ll x){
    ll idx = -1;
    while (x){
        idx+=1;
        x>>=1;
    }
    cnt[idx]++;
    // return idx
}


void solve(){
    cin >> T;
    while (T--){
        cin >> m>>n;
        ll sum=0;
        memset (cnt,0,sizeof cnt);
        for (ll i = 1;i<=n;++i){
            cin >> f[i];
            sum += f[i];
            add(f[i]);
        }
        if (sum<m){
            cout << -1<<endl;
        }
        else {
            cout << calc()<<endl;
        }
    
    }

}

int main(){
    
    // freopen("input.txt","r",stdin);
    // freopen("output.txt","w",stdout);
    io;
 
    solve();
    return 0;
}
```
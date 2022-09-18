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

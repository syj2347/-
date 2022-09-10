---
tags: [Code]
title: 网络流（ISAP）
created: '2022-09-02T13:10:22.156Z'
modified: '2022-09-02T13:10:50.230Z'
---

# 网络流（ISAP）
```cpp
#include <bits/stdc++.h>

using namespace std;

const int N = 100;          //点数，从1开始编号
const int M = 100000;       //边数
const int inf = 1000000000; //无穷大
struct E
{
    int t, f;
    E *nxt, *pair;
} * g[N], *d[N], pool[M * 2], *cur = pool;

int n, m, i, S, T, h[N], gap[N], maxflow;

void add(int s, int t, int f)
{ //添加s->t的一条边，容量为f
    E *p = cur++;
    p->t = t;
    p->f = f;
    p->nxt = g[s];
    g[s] = p;
    p = cur++;
    p->t = s;
    p->f = 0;
    p->nxt = g[t];
    g[t] = p;
    g[s]->pair = g[t];
    g[t]->pair = g[s];
}

int sap(int v, int flow)
{
    if (v == T)
        return flow;
    int rec = 0;
    for (E *p = d[v]; p; p = p->nxt)
        if (h[v] == h[p->t] + 1 && p->f)
        {
            int ret = sap(p->t, min(flow - rec, p->f));
            p->f -= ret;
            p->pair->f += ret;
            d[v] = p;
            if ((rec += ret) == flow)
                return flow;
        }
    if (!(--gap[h[v]]))
        h[S] = T;
    gap[++h[v]]++;
    d[v] = g[v];
    return rec;
}

void solve(int id)
{
    //S = n + 1; //源点
    //T = S + 1; //汇点
    S=1;
    T=n;
    for (cur = pool, i = 1; i <= T; i++)
        g[i] = d[i] = NULL, h[i] = gap[i] = 0; //初始化

    //请在这里连边
    for (int j = 1; j <= m; j++)
    {
        int s, t, f;
        cin >> s >> t >> f;
        add(s, t, f);
    }

    for (gap[maxflow = 0] = T, i = 1; i <= T; i++)
        d[i] = g[i];
    while (h[S] < T)
        maxflow += sap(S, inf);
    cout << maxflow <<"\n";
}

int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    int tt;
    cin >> tt;
    for (int i = 1; i <= tt; i++)
    {
        cin >> n >> m;
        solve(i);
    }
    return 0;
}
```

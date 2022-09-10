---
tags: [Code]
title: Dij堆优化
created: '2022-09-02T13:12:23.096Z'
modified: '2022-09-02T13:12:43.987Z'
---

# Dij堆优化
```cpp
// Dij模板
//注意从1开始存到n
#include <bits/stdc++.h>

using namespace std;

#define inf 2147483647
const int maxn = 5e5 + 5;
int n, m, s, e;
int cnt, head[maxn];
int dist[maxn], vis[maxn];
struct edge
{
    int to, dis, next;
} edge[maxn * 2];
void add(int from, int to, int w)
{
    edge[++cnt].to = to;
    edge[cnt].dis = w;
    edge[cnt].next = head[from];
    head[from] = cnt;
}
struct node
{
    int id, dis;
    bool operator<(const node &a) const { return a.dis < dis; }
};
void Dij()
{
    priority_queue<node> q;
    q.push(node{s, 0});
    for (int i = 1; i <= n; i++)
        dist[i] = inf;
    dist[s] = 0;
    while (!q.empty())
    {
        node a = q.top();
        q.pop();
        int now = a.id;
        if (vis[now])
            continue;
        vis[now] = 1;
        for (int i = head[now]; i; i = edge[i].next)
        {
            int j = edge[i].to;
            if (dist[now] + edge[i].dis < dist[j])
            {
                dist[j] = dist[now] + edge[i].dis;
                q.push(node{j, dist[j]});
            }
        }
    }
}
void init()
{
    cnt = 0;
    memset(head, 0, sizeof(head));
    memset(vis, 0, sizeof(vis));
}
int main()
{
    ios::sync_with_stdio(false);
    cin.tie(0);
    cout.tie(0);
    while (cin >> n >> m)
    {
        init();
        while (m--)
        {
            int a, b, x;
            cin >> a >> b >> x;
            a++, b++;
            add(a, b, x);
            add(b, a, x);
        }
        cin >> s >> e;
        s++, e++;
        Dij();
        if (dist[e] != inf)
            cout << dist[e] << "\n";
        else
            cout << "-1\n";
    }
    return 0;
}
```

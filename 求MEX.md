---
tags: [Code]
title: 求MEX
created: '2022-09-02T12:58:26.720Z'
modified: '2022-09-02T13:03:16.558Z'
---

# 求MEX
```cpp
const int N=200010;
int a[N];
int ct[N];
int r[N];
//int b[N];
int n;
void solve()
{
	cin >> n;
	memset(ct, 0, sizeof(ct));
	//memset(b, 0, sizeof(b));
	memset(r, 0, sizeof(r));
	for (int i = 1; i <= n; i++) {
		cin >> a[i];
		ct[a[i]]++;
	}
	int id = 1;
	int m = 0;
	for (int i = 1; i <= n; i++) {
		ct[a[i]]--;
		r[a[i]] = id;
		while (r[m] == id)
			m++;
		if (ct[m] == 0)
		{
			//b[id] = m;
			//id++;
			//m = 0;
            break;
		}
	}
    cout<<m<<endl;
}
```

---
tags: [Code]
title: C无序排列组合，结果取模d
created: '2022-09-02T13:09:00.745Z'
modified: '2022-09-02T13:09:39.937Z'
---

# C无序排列组合，结果取模d
```cpp
typedef long long ll;
const int d = 1e9 + 7;

ll fastpow(ll a, ll k)
{
	ll res = 1;
	while (k) {
		if (k & 1)res = res * a % d;
		a = a * a % d;
		k >>= 1;
	}
	return res;
}
ll C(ll b, ll a)
{
	ll res = 1;
	if (a > b || b == 0)return 0;
	if (a == b || a == 0)return 1;
	for (int i = 1; i <= a; i++) {
		res = (((res % d) * ((b - i + 1) % d)) % d * fastpow(i, d - 2)) % d;
	}
	return res;
}
```

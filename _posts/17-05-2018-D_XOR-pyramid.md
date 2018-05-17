---
layout: post
title: today still need to learn one
---
## {{ page.title }}
我的第二篇文章

```c++
#include <bits/stdc++.h>

using namespace std;

int f[5003][5003];
int a[5003];

int main() {
  ios::sync_with_stdio(false);cin.tie(0);cout.tie(0);
  int n;
  cin >> n;
  for(int i = 0; i < n; i += 1) {
    cin >> a[i];
    f[0][i] = a[i];
  }
  for(int i = 1; i < n; i += 1) {
    for(int j = 0; j <= n - i; j += 1) {
      f[i][j] = f[i - 1][j + 1] ^ f[i - 1][j];
    }
  }
  for(int i = 1; i < n; i += 1) {
    for(int j = 0; j < n - i; j += 1) {
      f[i][j] = max(max(f[i][j], f[i - 1][j]), f[i - 1][j + 1]);
    }
  }
  int q;
  cin >> q;
  for(int i = 0; i < q; i += 1) {
    int l, r;
    cin >> l >> r;
    cout << f[r - l][l - 1] << endl;
  }
  return 0;
}
```

{{ page.date | date_to_string }}
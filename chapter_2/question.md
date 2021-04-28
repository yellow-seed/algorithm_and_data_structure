
```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  int maxv = -200000;
  int minv = 200001;
  cin >> n;
  
  vector<int> r(n);

  for(int i = 0; i < n; i++){
    cin >> r[i];
  }

  for(int i = 0; i < n; i++) {
    maxv = max(maxv, maxv - r[i]);
    minv = min(minv, r[i]);
  }

  cout << maxv << endl;

  return 0;
}
```

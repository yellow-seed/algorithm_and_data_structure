11.2

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;

  vector<int> f(50);
  f[0] = f[1] = 1;

  for(int i = 2; i <= n; i++){
    f[i] = f[i - 1] + f[i - 2];
  }

  cout << f[n] << endl;
  
  return 0;
}
```

11.3

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000;

int lcs(string x, string y){
  vector<vector<int>> c(MAX + 1, vector<int>(MAX + 1));
  int m = x.size();
  int n = y.size();
  int maxl = 0;
  x = ' ' + x;
  y = ' ' + y;
  for(int i = 0; i <= m; ++i) c[i][0] = 0;
  for(int j = 0; j <= n; ++j) c[0][j] = 0;

  for(int i = 1; i <= m; ++i){
    for(int j = 1; j <= n; ++j){
      if(x[i] == y[j]){
        c[i][j] = c[i - 1][j - 1] + 1;
      }else{
        c[i][j] = max(c[i - 1][j], c[i][j - 1]);
      }
      maxl = max(maxl, c[i][j]);
    }
  }
  return maxl;
}

int main() {
  int q;
  string x, y;
  cin >> q;

  for(int i = 0; i < q; ++i){
    cin >> x >> y;
    cout << lcs(x, y) << endl;
  }

  return 0;
}
```

11.4

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;
  int p[n + 1], m[n + 1][n + 1];

  for(int i = 1; i <= n; ++i){
    cin >> p[i - 1] >> p[i];
    m[i][i] = 0;
  }

  for(int l = 2; l <= n; l++){
    for(int i = 1; i <= n - l + 1; i++){
      int j = i + l - 1;
      m[i][j] = __INT_MAX__;
      for(int k = i; k < j; k++){
        m[i][j] = min(m[i][j], m[i][k] + m[k + 1][j] + p[i - 1] * p[k] * p[j]);
      }
    }
  }

  cout << m[1][n] << endl;

  return 0;
}
```
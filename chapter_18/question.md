18.1

```
#include <bits/stdc++.h>
using namespace std;

bool isPrime(int x){
  if(x < 2) return false;
  else if(x == 2) return true;

  if(x % 2 == 0) return false;

  for(int i = 3; i * i <= x; i += 2){
    if(x % i == 0) return false;
  }
  return true;
}

int main() {
  int n;
  int cnt = 0;
  cin >> n;

  for(int i = 0; i < n; i++){
    int x;
    cin >> x;
    if(isPrime(x)) cnt++;
  }

  cout << cnt << endl;

  return 0;
}
```

18.2

```
#include <bits/stdc++.h>
using namespace std;

int gcd(int x, int y){
  if(x < y) swap(x, y);
  return y ? gcd(y, x % y) : x;
}

int main() {
  int a, b;
  cin >> a >> b;

  cout << gcd(a, b) << endl;

  return 0;
}
```

18.3

```
#include <bits/stdc++.h>
using namespace std;

long long power(long long x, long long n, long long M){
  long long res = 1;
  if(n > 0){
    res = power(x, n / 2, M);
    if(n % 2 == 0){
      res = (res * res) % M;
    }else{
      res = (((res * res) % M) * x) % M;
    }
  }
  return res;
}

int main() {
  int m, n;
  cin >> m >> n;

  cout << power(m, n, 1000000007) << endl;

  return 0;
}
```
5.2

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n, q;
  cin >> n;

  vector<int> s(n);
  for(int i = 0; i < n; i++){cin >> s[i];}

  cin >> q;

  vector<int> t(q);
  for(int i = 0; i < q; i++){cin >> t[i];}

  int c = 0;
  for(int i = 0; i < q; i++){
    int j = 0;
    while(s[j] != t[i]){
      j++;
    }
    if(j != n){c++;}
  }

  cout << c << endl;
  

  return 0;
}
```

5.3

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n, q;
  cin >> n;

  vector<int> s(n);
  for(int i = 0; i < n; i++){cin >> s[i];}

  cin >> q;

  vector<int> t(q);
  for(int i = 0; i < q; i++){cin >> t[i];}

  int c = 0;

  for(int i = 0; i < q; i++){
    int left = 0;
    int right = n;
    int mid;
    while(left < right){
      mid = (left + right) / 2;
      if(s[mid] == t[i]){
        c++;
        break;
      } else if(t[i] < s[mid]){
        right = mid;
      } else {
        left = mid + 1;
      }
    }
  }

  cout << c << endl;
  

  return 0;
}
```

5.4

```
#include <bits/stdc++.h>
using namespace std;
const long M = 1046527;
const int NIL = -1;

long T[M];

int getChar(char ch){
  if(ch == 'A') return 1;
  else if(ch == 'C') return 2;
  else if(ch == 'G') return 3;
  else if(ch == 'T') return 4;
}

long getKey(string str){
  long sum = 0, p = 1;
  for(int i = 0; i < str.size(); i++){
    sum += p * getChar(str[i]);
    p *= 5;
  }
  return sum;
}

long h1(long key){
  return key % M;
}

long h2(long key){
  return 1 + (key % (M - 1));
}

long h(long key, int i){
  return (h1(key) + i * h2(key)) % M;
}

int insert(long key){
  long hash;
  for(int i = 0; ; i++){
    hash = h(key, i);
    if (hash >= M) return 0;

    if (T[hash] == NIL){
      T[hash] = key;
      return 1;
    }
  }
}

int find(long key){
  long hash;
  for(int i = 0; ; i++){
    hash = h(key, i);
    if(hash >= M - 1) return 0;

    if(T[hash] == key){
      return 1;
    }
  }
}

int main() {
  for(int i = 0; i < M; i++) T[i] = NIL;

  int n;
  cin >> n;

  string cmd, str;
  long key;

  for(int i = 0; i < n; i++){
    cin >> cmd >> str;
    key = getKey(str);

    if(cmd[0] == 'i'){
      insert(key);
    } else if(cmd[0] == 'f'){
      if(find(key)){
        cout << "yes" << endl;
      } else {
        cout << "no" << endl;
      }
    }
  }

  return 0;
}
```

5.6

```
```


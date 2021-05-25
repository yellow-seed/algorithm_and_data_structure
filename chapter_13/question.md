13.2

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;
const int WHITE = 0;
const int GRAY = 1;
const int BLACK = 2;
int n, M[MAX][MAX];

int prim(){
  int d[MAX], p[MAX], color[MAX];
  int minv, u;
  for(int i = 0; i < n; ++i){
    d[i] = INT_MAX;
    p[i] = -1;
    color[i] = WHITE;
  }

  d[0] = 0;

  while(true){
    minv = INT_MAX;
    u = -1;
    for(int i = 0; i < n; ++i){
      if(minv > d[i] && color[i] != BLACK){
        u = i;
        minv = d[i];
      }
    }
    if(u == -1) break;
    color[u] = BLACK;
    for(int v = 0; v < n; v++){
      if(color[v] != BLACK && M[u][v] != INT_MAX){
        if(d[v] > M[u][v]){
          d[v] = M[u][v];
          p[v] = u;
          color[v] = GRAY;
        }
      }
    }
  }
  int sum = 0;
  for(int i = 0; i < n; ++i){
    if(p[i] != -1) sum += M[i][p[i]];
  }
  return sum;
}

int main() {
  cin >> n;

  for(int i = 0; i < n; ++i){
    for(int j = 0; j < n; ++j){
      int e;
      cin >> e;
      M[i][j] = (e == -1) ? INT_MAX : e;
    }
  }

  cout << prim() << endl;

  return 0;
}
```

13.3 B

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;
const int WHITE = 0;
const int GRAY = 1;
const int BLACK = 2;
int n, M[MAX][MAX];

void dijakstra(){
  int minv;
  int d[MAX], color[MAX];

  for(int i = 0; i < n; ++i){
    d[i] = INT_MAX;
    color[i] = WHITE;
  }

  d[0] = 0;
  color[0] = GRAY;

  while(true){
    minv = INT_MAX;
    int u = -1;
    for(int i = 0; i < n; i++){
      //d[i]が最大値以外 かつ 探査未完了
      if(minv > d[i] && color[i] != BLACK){
        u = i;
        minv = d[i];
      }
    }
    // 辺がなければ次へ
    if(u == -1) break;

    color[u] = BLACK;
    for(int v = 0; v < n; v++){
      // 探査終点が探査未完了 かつ 辺は存在する
      if(color[v] != BLACK && M[u][v] != INT_MAX){
        if(d[v] > d[u] + M[u][v]){
          d[v] = d[u] + M[u][v];
          color[v] = GRAY;
        }
      }
    }
  }
  for(int i = 0; i < n; ++i){
    cout << i << " " << (d[i] == INT_MAX ? -1 : d[i]) << endl;
  }
}

int main() {
  cin >> n;

  for(int i = 0; i < n; i++){
    for(int j = 0; j < n; j++){
      M[i][j] = INT_MAX;
    }
  }

  int u, k, v, c;
  for(int i = 0; i < n; i++){
    cin >> u >> k;
    for(int j = 0; j < k; j++){
      cin >> v >> c;
      M[u][v] = c;
    }
  }

  dijakstra();

  return 0;
}
```

13.3 C

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;
const int WHITE = 0;
const int GRAY = 1;
const int BLACK = 2;
int n;
vector<pair<int, int>> adj[MAX];

void dijakstra(){
  priority_queue<pair<int, int>> PQ;
  int color[MAX];
  int d[MAX];

  for(int i = 0; i < n; i++){
    d[i] = INT_MAX;
    color[i] = WHITE;
  }

  d[0] = 0;
  PQ.push(make_pair(0, 0));
  color[0] = GRAY;

  while(!PQ.empty()){
    pair<int, int> f = PQ.top();
    PQ.pop();
    int u = f.second;
    color[u] = BLACK;

    if(d[u] < f.first * (-1)) continue;
    
    for(int j = 0; j < adj[u].size(); j++){
      int v = adj[u][j].second;

      if(color[v] == BLACK) continue;

      if(d[v] > d[u] + adj[u][j].first){
        d[v] = d[u] + adj[u][j].first;
        PQ.push(make_pair(d[v] * -1, v));
        color[v] = GRAY;
      }
    }
  }
  for(int i = 0; i < n; i++){
    cout << i << " " << (d[i] == INT_MAX ? -1 : (d[i])) << endl;
  }
}

int main() {
  cin >> n;

  int u, k, v, c;
  for(int i = 0; i < n; i++){
    cin >> u >> k;
    for(int j = 0; j < k; j++){
      cin >> v >> c;
      adj[u].push_back(make_pair(c, v));
    }
  }

  dijakstra();

  return 0;
}
```
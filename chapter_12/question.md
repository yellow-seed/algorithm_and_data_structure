12.2

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;
  int u, k, v;

  vector<vector<int>> m(n, vector<int>(n));

  for(int i = 0; i < n; ++i){
    for(int j = 0; j < n; ++j) m[i][j] = 0;
  } 

  for(int i = 0; i < n; ++i){
    cin >> u >> k;
    u--;
    for(int j = 0; j < k; ++j){
      cin >> v;
      v--;
      m[u][v] = 1;
    }
  }

  for(int i = 0; i < n; ++i){
    for(int j = 0; j < n; ++j){
      if(j) cout << " ";
      cout << m[i][j];
    }
    cout << endl;
  }

  return 0;
}
```

12.3

```
#include <bits/stdc++.h>
using namespace std;

const int N = 100;
const int WHITE = 0;
const int GRAY = 1;
const int BLACK = 2;
int m[N][N];
int color[N], d[N], f[N];
int n, tt;

void dfs_visit(int i){
  color[i] = GRAY;
  d[i] = ++tt;

  for(int j = 0; j < n; ++j){
    if(m[i][j] == 0) continue;
    if(color[j] == WHITE) dfs_visit(j);
  }
  color[i] = BLACK;
  f[i] = ++tt;
}

void dfs(){
  for(int i = 0; i < n; ++i){
    color[i] = WHITE;
  }
  tt = 0;

  for(int i = 0; i < n; ++i){
    if(color[i] == WHITE) dfs_visit(i);
  }

  for(int i = 0; i < n; ++i){
    cout << i + 1 << " " << d[i] << " " << f[i] << endl;
  }
}

int main() {
  int u, k, v;
  cin >> n;
  

  for(int i = 0; i < n; ++i){
    for(int j = 0; j < n; ++j) m[i][j] = 0;
  }

  for(int i = 0; i < n; ++i){
    cin >> u >> k;
    u--;
    for(int j = 0; j < k; ++j){
      cin >> v;
      v--;
      m[u][v] = 1;
    }
  }

  dfs();

  return 0;
}
```

12.4

```
#include <bits/stdc++.h>
using namespace std;

const int N = 100;
int m[N][N];
int d[N];
int n;

void bfs(int s){
  queue<int> q;
  q.push(s);

  for(int i = 0; i < n; ++i) d[i] = __INT_MAX__;

  d[s] = 0;
  while(!q.empty()){
    int u = q.front();
    q.pop();
    for(int v = 0; v < n; ++v){
      if(m[u][v] == 0) continue;
      if(d[v] != __INT_MAX__) continue;
      d[v] = d[u] + 1;
      q.push(v);
    }
  }
  for(int i = 0; i < n; ++i){
    cout << i + 1 << " " << (d[i] == __INT_MAX__ ? (-1) : d[i]) << endl;
  }
}

int main() {
  int u, k, v;
  cin >> n;

  for(int i = 0; i < n; ++i){
    for(int j = 0; j < n; ++j) m[i][j] = 0;
  }

  for(int i = 0; i < n; ++i){
    cin >> u >> k;
    u--;
    for(int j = 0; j < k; ++j){
      cin >> v;
      v--;
      m[u][v] = 1;
    }
  }

  bfs(0);

  return 0;
}
```

12.5

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;
const int NIL = -1;
int n;
vector<int> G[MAX];
vector<int> color(MAX);

void dfs(int r, int id){
  stack<int> S;
  S.push(r);
  color[r] = id;

  while(!S.empty()){
    int u = S.top();
    S.pop();
    for(int i = 0; i < G[u].size(); ++i){
      int v = G[u][i];
      if(color[v] == NIL){
        color[v] = id;
        S.push(v);
      }
    }
  }
}

void assignColor(){
  int id = 1;
  for(int i = 0; i < n; i++){
    color[i] = NIL;
  }

  for(int i = 0; i < n; i++){
    if(color[i] == NIL) dfs(i, id++);
  }
}

int main() {
  int m, q;
  int s, t;
  cin >> n >> m;

  for(int i = 0; i < m; ++i){
    cin >> s >> t;
    G[s].push_back(t);
    G[t].push_back(s);
  }

  assignColor();

  cin >> q;

  for(int i = 0; i < q; i++){
    cin >> s >> t;
    if(color[s] == color[t]){
      cout << "yes" << endl;
    }else{
      cout << "no" << endl;
    }
  }

  return 0;
}
```
15.1

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100;
const int NIL = -1;
int n;
long long dd[MAX][MAX];

void floyd(){
  for(int k = 0; k < n; k++){
    for(int i = 0; i < n; i++){
      if(dd[i][k] == INT_MAX) continue;
      for(int j = 0; j < n; j++){
        if(dd[k][j] == INT_MAX) continue;
        dd[i][j] = min(dd[i][j], dd[i][k] + dd[k][j]);
      }
    }
  }
}

int main() {
  int v, e;
  int s, t, d;
  cin >> n >> e;

  for(int i = 0; i < n; i++){
    for(int j = 0; j < n; j++){
      dd[i][j] = ((i == j) ? 0 : INT_MAX);
    }
  }

  for(int i = 0; i < e; i++){
    cin >> s >> t >> d;
    dd[s][t] = d;
  }

  floyd();

  bool negative = false;
  for(int i = 0; i < n; i++) if(dd[i][i] < 0) negative = true;

  if(negative){
    cout << "NEGATIVE CYCLE" << endl;
  }else{
    for(int i = 0; i < n; i++){
      for(int j = 0; j < n; j++){
        if(j) cout << " ";
        if(dd[i][j] == INT_MAX) cout << "INF";
        else cout << dd[i][j];
      }
      cout << endl;
    }
  }

  return 0;
}
```

15.2

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;
const int NIL = -1;

int N;
vector<int> G[MAX];
list<int> out;
bool V[MAX];
int indeg[MAX];

void bfs(int s){
  queue<int> q;
  q.push(s);
  V[s] = true;

  while(!q.empty()){
    int u = q.front();
    q.pop();

    out.push_back(u);
    for(int i = 0; i < G[u].size(); i++){
      int v = G[u][i];
      indeg[v]--;
      if(indeg[v] == 0 && !V[v]){
        V[v] = true;
        q.push(v);
      }
    }
  }
}

void toposort(){
  for(int i = 0; i < N; i++){
    indeg[i] = 0;
  }

  for(int u = 0; u < N; u++){
    for(int i = 0; i < G[u].size(); i++){
      int v = G[u][i];
      indeg[v]++;
    }
  }

  for(int u = 0; u < N; u++){
    if(indeg[u] == 0 && !V[u]) bfs(u);
  }

  for(list<int>::iterator it = out.begin(); it != out.end(); it++){
    cout << *it << endl;
  }
}

int main() {
  int s, t, E;
  cin >> N >> E;

  for(int i = 0; i < N; i++) V[i] = false;

  for(int i = 0; i < E; i++){
    cin >> s >> t;
    G[s].push_back(t);
  }

  toposort();

  return 0;
}
```

15.3

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;
const int NIL = -1;

int N;
int timer;
vector<int> G[MAX];
bool visited[MAX];
int prenum[MAX], lowest[MAX], parent[MAX];

void dfs(int current, int prev){
  prenum[current] = lowest[current] = timer;
  timer++;
  visited[current] = true;

  int next;
  for(int i = 0; i < G[current].size(); i++){
    next = G[current][i];
    if(!visited[next]){
      parent[next] = current;
      dfs(next, current);
      lowest[current] = min(lowest[current], lowest[next]);
    }else if(next != prev){
      // 後退辺
      lowest[current] = min(lowest[current], prenum[next]);
    }
  }
}

void artPoint(){
  for(int i = 0; i < N; i++){
    visited[i] = false;
  }
  timer = 1;
  dfs(0, -1);

  set<int> ap;
  int np = 0;

  for(int i = 1; i < N; i++){
    int p = parent[i];
    if(p == 0) np++;
    else if(prenum[p] <= lowest[i]) ap.insert(p);
  }
  if(np > 1) ap.insert(0);
  for(set<int>::iterator it = ap.begin(); it != ap.end(); it++){
    cout << *it <<endl;
  }
}

int main() {
  int E;
  cin >> N >> E;

  for(int i = 0; i < E; i++){
    int s, t;
    cin >> s >> t;
    G[s].push_back(t);
    G[t].push_back(s);
  }

  artPoint();

  return 0;
}
```

15.4

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;
const int NIL = -1;

struct Edge{
  int t, w;
  Edge(){}
  Edge(int t, int w): t(t), w(w) {}
};

int n;
int d[MAX];
vector<Edge> G[MAX];

void bfs(int s){
  for(int i = 0; i < n; i++) d[i] = INT_MAX;
  queue<int> Q;
  Q.push(s);
  d[s] = 0;

  while(!Q.empty()){
    int u = Q.front();
    Q.pop();
    for(int i = 0; i < G[u].size(); i++){
      Edge e = G[u][i];
      if(d[e.t] == INT_MAX){
        d[e.t] = d[u] + e.w;
        Q.push(e.t);
      }
    }
  }
}

void solve(){
  bfs(0);
  int maxv;
  int target;

  for(int i = 0; i < n; i++){
    if(d[i] == INT_MAX) continue;
    if(maxv < d[i]){
      maxv = d[i];
      target = i;
    }
  }

  bfs(target);
  maxv = 0;

  for(int i = 0; i < n; i++){
    if(d[i] == INT_MAX) continue;
    maxv = max(maxv, d[i]);
  }

  cout << maxv << endl;
}

int main() {
  int s, t, w;
  cin >> n;

  for(int i = 1; i <= n - 1; i++){
    cin >> s >> t >> w;

    G[s].push_back(Edge(t, w));
    G[t].push_back(Edge(s, w));
  }

  solve();

  return 0;
}
```

15.5

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;
const int NIL = -1;

struct DisjoinSet{
  vector<int> rank, parent;

  DisjoinSet(){}
  DisjoinSet(int size){
    rank.resize(size, 0);
    parent.resize(size, 0);
    for(int i = 0; i < size; i++) makeSet(i);
  }

  void makeSet(int x){
    parent[x] = x;
    rank[x] = 0;
  }

  bool same(int x, int y){
    return findSet(x) == findSet(y);
  }

  void unite(int x, int y){
    link(findSet(x), findSet(y));
  }

  void link(int x, int y){
    if(rank[x] > rank[y]){
      parent[y] = x;
    }else{
      parent[x] = y;
      if(rank[x] == rank[y]){
        rank[y]++;
      }
    }
  }

  int findSet(int x){
    if(x != parent[x]){
      parent[x] = findSet(parent[x]);
    }
    return parent[x];
  }
};

struct Edge{
  int source, target, cost;
  Edge(int source = 0, int target = 0, int cost = 0): source(source), target(target), cost(cost){}

  bool operator < (const Edge &e) const {
    return cost < e.cost;
  }
};

int kruskal(int N, vector<Edge> edges){
  int totalCost = 0;
  sort(edges.begin(), edges.end());

  DisjoinSet dset = DisjoinSet(N + 1);
  for(int i = 0; i < N; i++) dset.makeSet(i);

  int source, target;

  for(int i = 0; i < edges.size(); i++){
    Edge e = edges[i];
    if(!dset.same(e.source, e.target)){
      totalCost += e.cost;
      dset.unite(e.source, e.target);
    }
  }
  return totalCost;
}

int main() {
  int V, E;
  int s, t, w;
  cin >> V >> E;

  vector<Edge> edges;
  for(int i = 0; i < E; i++){
    cin >> s >> t >> w;
    edges.push_back(Edge(s, t, w));
  }

  cout << kruskal(V, edges) << endl;

  return 0;
}
```
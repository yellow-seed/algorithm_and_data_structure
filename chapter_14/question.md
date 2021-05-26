14.1

```
#include <bits/stdc++.h>
using namespace std;

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

int main() {
  int n, q;
  int x, y;
  int com;
  cin >> n >> q;

  DisjoinSet ds = DisjoinSet(n);

  for(int i = 0; i < q; i++){
    cin >> com >> x >> y;
    if(com == 0) ds.unite(x, y);
    else if(com == 1){
      if(ds.same(x, y)) cout << 1 << endl;
      else cout << 0 << endl;
    }
  }

  return 0;
}
```

14.2

```
#include <bits/stdc++.h>
using namespace std;

struct Node{
  int location;
  int parent, left, right;
  Node(){}
};

struct Point{
  int id, x, y;
  Point(){}
  Point(int id, int x, int y): id(id), x(x), y(y){}

  bool operator < (const Point &p) const {
    return id < p.id;
  }
  
  void print(){
    cout << id << endl;
  }
};

const int MAX = 1000000;
const int NIL = -1;
int n;
Point P[MAX];
Node T[MAX];
int np;

// 構造体メンバ変数のソートで利用するpredicate
bool lessX(const Point &p1, const Point &p2){return p1.x < p2.x;}
bool lessY(const Point &p1, const Point &p2){return p1.y < p2.y;}

int makeKDTree(int l, int r, int depth){
  if(!(l < r)) return NIL;

  int mid = (l + r) / 2;
  //t:二分探索木node番号
  int t = np++;
  //x軸y軸判定
  if(depth % 2 == 0){
    sort(P + l, P + r, lessX);
  }else{
    sort(P + l, P + r, lessY);
  }

  T[t].location = mid;
  T[t].left = makeKDTree(l, mid, depth + 1);
  T[t].right = makeKDTree(mid + 1, r, depth + 1);

  return t;
}

void find(int v, int sx, int tx, int sy, int ty, int depth, vector<Point> &ans){
  int x = P[T[v].location].x;
  int y = P[T[v].location].y;

  if(sx <= x && x <= tx && sy <= y && y <= ty){
    ans.push_back(P[T[v].location]);
  }

  if(depth % 2 == 0){
    if(T[v].left != NIL){
      if(sx <= x) find(T[v].left, sx, tx, sy, ty, depth + 1, ans);
    }
    if(T[v].right != NIL){
      if(x <= tx) find(T[v].right, sx, tx, sy, ty, depth + 1, ans);
    }
  }else{
    if(T[v].left != NIL){
      if(sy <= y) find(T[v].left, sx, tx, sy, ty, depth + 1, ans);
    }
    if(T[v].right != NIL){
      if(y <= ty) find(T[v].right, sx, tx, sy, ty, depth + 1, ans);
    }
  }
}

int main() {
  int x, y;
  cin >> n;

  for(int i = 0; i < n; i++){
    cin >> x >> y;
    P[i] = Point(i, x, y);
    T[i].left = T[i].right = T[i].parent = NIL; 
  }

  np = 0;
  int root = makeKDTree(0, n, 0);

  int q;
  cin >> q;
  int sx, tx, sy, ty;
  vector<Point> ans;

  for(int i = 0; i < q; i++){
    cin >> sx >> tx >> sy >> ty;
    ans.clear();
    find(root, sx, tx, sy, ty, 0, ans);
    sort(ans.begin(), ans.end());

    for(int j = 0; j < ans.size(); j++){
      ans[j].print();
    }
    cout << endl;
  }

  return 0;
}
```
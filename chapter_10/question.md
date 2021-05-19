10.2

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100000;

struct Node{
  int key;
  Node *parent, *left, *right;
};

int parent(int key){
  return key / 2;
}

int left(int key){
  return 2 * key;
}

int right(int key){
  return 2 * key + 1;
}

int main() {
  int n;
  cin >> n;
  vector<int> a(MAX);

  for(int i = 1; i <= n; ++i) cin >> a[i];

  for(int i = 1; i <= n; ++i){
    cout << "node " << i << ": key = " << a[i] << ", ";
    if(parent(i) >= 1) cout << "parent key = " << a[parent(i)] << ", ";
    if(left(i) <= n) cout << "left key = " << a[left(i)] << ", ";
    if(right(i) <= n) cout << "right key = " << a[right(i)] << ", ";
    cout << endl;
  }
  
  return 0;
}
```

10.3

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100000;

vector<int> a(MAX);

void maxHeapify(int key, int n){
  int l, r, largest;
  l = 2 * key;
  r = 2 * key + 1;

  if(l <= n && a[l] > a[key]) largest = l;
  else largest = key;
  
  if(r <= n && a[r] > a[largest]) largest = r;

  if(largest != key){
    swap(a[key], a[largest]);
    maxHeapify(largest, n);
  }
}

int main() {
  int n;
  cin >> n;

  for(int i = 1; i <= n; i++) cin >> a[i];

  for(int i = n / 2; i >= 1; i--) maxHeapify(i, n);

  for(int i = 1; i <= n; i++){
    cout << " " << a[i];
  }
  cout << endl;
  
  return 0;
}
```

10.4

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100000;
const int INFTY = (1<<30);

vector<int> a(MAX);
int n;

int parent(int i){
  return i / 2;
}

void maxHeapify(int key){
  int l, r, largest;
  l = 2 * key;
  r = 2 * key + 1;

  if(l <= n && a[l] > a[key]) largest = l;
  else largest = key;
  
  if(r <= n && a[r] > a[largest]) largest = r;

  if(largest != key){
    swap(a[key], a[largest]);
    maxHeapify(largest);
  }
}

void increaseKey(int i, int key){
  if(key < a[i]) return;
  a[i] = key;
  while(i > 1 && a[parent(i)] < a[i]){
    swap(a[i], a[parent(i)]);
    i = parent(i);
  }
}

void insert(int key){
  n++;
  a[n] = -INFTY;
  increaseKey(n, key);
}

int extract(){
  int maxv;
  if(n < 1) return -INFTY;
  maxv = a[1];
  a[1] = a[n--];
  maxHeapify(1);
  return maxv;
}

int main() {
  string com;
  int key;

  while(1){
    cin >> com;
    if(com == "end") break;
    if(com == "insert"){
      cin >> key;
      insert(key);
    }else{
      cout << extract() << endl;
    }
  }
  
  return 0;
}
```
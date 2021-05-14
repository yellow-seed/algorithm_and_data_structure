7.1

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 500000;
const int INFTY = 2000000000;

int n;
int cnt;
int L[MAX / 2], R[MAX / 2];

void merge(int a[], int left, int mid, int right){
  int n1 = mid - left;
  int n2 = right - mid;

  for(int i = 0; i < n1; i++){
    L[i] = a[left + i];
  }
  L[n1] = INFTY;

  for(int i = 0; i < n2; i++){
    R[i] = a[mid + i];
  }
  R[n2] = INFTY;

  int i = 0, j = 0;
  for(int k = left; k < right; k++){
    cnt++;
    if(L[i] <= R[j]){
      a[k] = L[i++];
    } else {
      a[k] = R[j++];
    }
  }
}

void mergeSort(int a[], int left, int right){
  if(left + 1 < right){
    int mid = (left + right) / 2;
    mergeSort(a, left, mid);
    mergeSort(a, mid, right);
    merge(a, left, mid, right);
  }
}

int main() {
  int A[MAX];
  cnt = 0;

  cin >> n;
  for (int i = 0; i < n; i++) {
    cin >> A[i];
  }

  mergeSort(A, 0, n);

  for (int i = 0; i < n; i++) {
    if (i) cout << " ";
    cout << A[i];
  }
  cout << endl;
  cout << cnt << endl;

  
  return 0;
}
```

7.2

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000000;
vector<int> a(MAX);

int partition(int p, int r){
  int x = a[r];
  int i = p - 1;
  for(int j = p; j < r; j++){
    if(a[j] <= x){
      i++;
      swap(a[i], a[j]);
    }
  }
  swap(a[i + 1], a[r]);
  return i + 1;
}

int main() {
  int n;
  cin >> n;

  for(int i = 0; i < n; i++) cin >> a[i];

  int q = partition(0, n -1);

  for(int i = 0; i < n; i++){
    if(i) cout << " ";
    if(i == q) cout << "[";
    cout << a[i];
    if(i == q) cout << "]";
  }
  cout << endl;
  
  return 0;
}
```

7.3

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1000000;
const int INFTY = 2000000000;

struct Card{
  char suit;
  int value;
};

Card L[MAX / 2], R[MAX / 2];

void merge(vector<Card> &a, int n, int left, int mid, int right){
  int n1 = mid - left;
  int n2 = right - mid;

  for(int i = 0; i < n1; i++){
    L[i] = a[left + i];
  }
  L[n1].value = INFTY;

  for(int i = 0; i < n2; i++){
    R[i] = a[mid + i];
  }
  R[n2].value = INFTY;

  int i = 0, j = 0;
  for(int k = left; k < right; k++){
    if(L[i].value <= R[j].value){
      a[k] = L[i++];
    } else {
      a[k] = R[j++];
    }
  }
}

void mergeSort(vector<Card> &a, int n, int left, int right){
  if(left + 1 < right){
    int mid = (left + right) / 2;
    mergeSort(a, n, left, mid);
    mergeSort(a, n, mid, right);
    merge(a, n, left, mid, right);
  }
}

int partition(vector<Card> &b, int n, int p, int r){
  Card x = b[r];
  int i = p - 1;
  for(int j = p; j < r; j++){
    if(b[j].value <= x.value){
      i++;
      swap(b[i], b[j]);
    }
  }
  swap(b[i + 1], b[r]);
  return i + 1;
}

void quickSort(vector<Card> &b, int n, int p, int r){
  if(p < r){
    int q = partition(b, n, p, r);
    quickSort(b, n, p, q - 1);
    quickSort(b, n, q + 1, r);
  }
}

int main() {
  int n,v;
  char s;
  bool stable = true;
  cin >> n;
  vector<Card> a(n), b(n);

  for(int i = 0; i < n; i++){
    cin >> s >> v;
    a[i].suit = b[i].suit = s;
    a[i].value = b[i].value = v;
  }

  mergeSort(a, n, 0, n);
  quickSort(b, n, 0, n - 1);

  for(int i = 0; i < n; i++){
    if(a[i].suit != b[i].suit) stable = false;
  }

  if(stable){
    cout << "Stable" << endl;
  } else {
    cout << "Not stable" << endl;
  }

  for(int i = 0; i < n; i++){
    cout << b[i].suit << " " << b[i].value << endl;
  }
  
  return 0;
}
```

7.4

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 10000;

int main() {
  int n;
  cin >> n;
  vector<int> a(n);
  for(int i = 0; i < n; i++){
    cin >> a[i];
  }
  vector<int> num(MAX);
  
  for(int i = 0; i < n; ++i){
    ++num[a[i]];
  }

  vector<int> sum(MAX);

  for(int v = 0; v <= MAX; ++v){
    sum[v] = sum[v - 1] + num[v];
  }

  vector<int> sorted(n);
  for(int i = n - 1; i >= 0; --i){
    sorted[--sum[a[i]]] = a[i];
  }

  for(int i = 0; i < sorted.size(); i++){
    cout << sorted[i] << " ";
  }
  cout << endl;

  
  return 0;
}
```

7.6

```
```

7.7

```
```
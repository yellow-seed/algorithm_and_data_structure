3.2

```
#include <bits/stdc++.h>
using namespace std;

int main() {
  int n;
  cin >> n;
  
  vector<int> a(n);

  for(int i = 0; i < n; i++){
    cin >> a[i];
  }

  // ソート前配列
  for(int i = 0; i < n; i++) cout << a[i] << " ";
  cout << endl;

  // 挿入ソート
  for(int i = 1; i < n; i++){
    int v = a[i];
    int j = i;
    while(j > 0 && a[j - 1] > v){
      a[j] = a[j - 1];
      j--;
    }
    a[j] = v;

    for(int i = 0; i < n; i++) cout << a[i] << " ";
    cout << endl;
  }

  return 0;
}
```

3.3

```
#include <bits/stdc++.h>
using namespace std;

void BubbleSort(vector<int> a, int counter) {
  for(int i = 0; i < a.size() - 1; i++){
    for(int j = (int)a.size() - 1; j > i; j--){
      if(a[j] < a[j - 1]){
        swap(a[j], a[j - 1]);
        counter++;
      }
    }
  }
  
  for(int i = 0;  i < a.size(); i++) cout << a[i] << " ";
  cout << endl;
  cout << counter << endl;
}

int main() {
  int n;
  cin >> n;
  int counter = 0;
  
  vector<int> a(n);

  for(int i = 0; i < n; i++){
    cin >> a[i];
  }

  // バブルソート
  BubbleSort(a, counter);

  return 0;
}
```

3.4

```
#include <bits/stdc++.h>
using namespace std;

void SelectionSort(vector<int> a, int counter) {
  for(int i = 0; i < a.size(); i++){
    int minj = i;
    for(int j = i; j < a.size(); j++){
      if(a[j] < a[minj]) {
        minj = j;
      }
    }
    if (i != minj) {
      swap(a[i], a[minj]);
      counter++;
    }
  }

  for(int i = 0;  i < a.size(); i++) cout << a[i] << " ";
  cout << endl;
  cout << counter << endl;
}

int main() {
  int n;
  cin >> n;
  int counter = 0;
  
  vector<int> a(n);

  for(int i = 0; i < n; i++){
    cin >> a[i];
  }

  // 選択ソート
  SelectionSort(a, counter);

  return 0;
}
```

3.5

```
```

3.6

```
```

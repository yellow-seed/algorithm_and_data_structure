17.1

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 20;
const int NMAX = 50000;

int main() {
  int n, m;
  int C[NMAX + 1];
  int T[NMAX + 1];

  cin >> n >> m;

  for(int i = 1; i <= m; i++) cin >> C[i];

  for(int i = 0; i <= NMAX; i++) T[i] = INT_MAX;
  T[0] = 0;

  for(int i = 1; i <= m; i++){
    for(int j = 0; j + C[i] <= n; j++){
      T[j + C[i]] = min(T[j + C[i]], T[j] + 1);
    }
  }

  cout << T[n] << endl;

  return 0;
}
```

17.2

```
#include <bits/stdc++.h>
using namespace std;

struct Item{
  int value, weight;
};

const int NMAX = 105;
const int WMAX = 10005;

Item items[NMAX];
int C[NMAX][WMAX];
int N, W;

int knapsack(){
  //C初期化
  for(int w = 0; w <= W; w++) C[0][w] = 0;

  for(int i = 1; i <= N; i++) C[i][0] = 0;

  for(int i = 1; i <= N; i++){
    for(int j = 1; j <= W; j++){
      C[i][j] = C[i - 1][j];
      if(items[i].weight > j) continue;
      if(items[i].value + C[i - 1][j - items[i].weight] > C[i - 1][j]){
        C[i][j] = items[i].value + C[i - 1][j - items[i].weight];
      }
    }
  }
  return C[N][W];
}

int main() {
  int maxValue;
  cin >> N >> W;

  for(int i = 1; i <= N; i++){
    cin >> items[i].value >> items[i].weight;
  }

  cout << knapsack() << endl;

  return 0;
}
```

17.3

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100000;

int n;
int A[MAX], L[MAX];

int LIS(){
  L[0] = A[0];
  int length = 1;

  for(int i = 1; i < n; i++){
    if(L[length - 1] < A[i]){
      L[length++] = A[i];
    }else{
      *lower_bound(L, L + length, A[i]) = A[i];
    }
  }
  return length;
}

int main() {
  cin >> n;

  for(int i = 0; i < n; i++){
    cin >> A[i];
  }

  cout << LIS() << endl;

  return 0;
}
```

17.4

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1400;

int n;
int C[MAX][MAX], dp[MAX][MAX];

int getLargestSquare(int H, int W){
  int maxWidth = 0;
  for(int i = 1; i < H; i++){
    for(int j = 1; j < W; j++){
      if(C[i][j]){
        //汚れ
        dp[i][j] = 0;
      }else{
        dp[i][j] = min(dp[i - 1][j - 1], min(dp[i - 1][j], dp[i][j - 1])) + 1;
        maxWidth = max(maxWidth, dp[i][j]);
      }
    }
  }
  return maxWidth * maxWidth;
}

int main() {
  int H, W;
  cin >> H >> W;

  for(int i = 0; i < H; i++){
    for(int j = 0; j < W; j++){
      cin >> C[i][j];
    }
  }

  cout << getLargestSquare(H, W) << endl;

  return 0;
}
```

17.5

```
#include <bits/stdc++.h>
using namespace std;

const int MAX = 1400;

struct Rectangle{
  int height;
  int pos;
};

int H, W;
int buffer[MAX][MAX], T[MAX][MAX];

int getLargestRectangle(int size, int buffer[]){
  stack<Rectangle> S;
  int maxv = 0;
  buffer[size] = 0;

  for(int i = 0; i <= size; i++){
    Rectangle rect;
    rect.height = buffer[i];
    rect.pos = i;

    if(S.empty()){
      S.push(rect);
    }else{
      if(S.top().height < rect.height){
        S.push(rect);
      }else if(S.top().height > rect.height){
        int target = i;
        while(!S.empty() && S.top().height >= rect.height){
          Rectangle pre = S.top();
          S.pop();
          int area =pre.height * (i - pre.pos);
          maxv = max(maxv, area); 
        }
        rect.pos = target;
        S.push(rect);
      }
    }
  }
  return maxv;
}

int getLargestRectangle(){
  for(int j = 0; j < W; j++){
    for(int i = 0; i < H; i++){
      if(buffer[i][j]){
        T[i][j] = 0;
      }else{
        T[i][j] = (i > 0) ? T[i - 1][j] + 1 : 1;
      }
    }
  }

  int maxv = 0;
  for(int i = 0; i < H; i++){
    maxv = max(maxv, getLargestRectangle(W, T[i]));
  }
  return maxv;
}

int main() {
  cin >> H >> W;

  for(int i = 0; i < H; i++){
    for(int j = 0; j < W; j++){
      cin >> buffer[i][j];
    }
  }

  cout << getLargestRectangle() << endl;

  return 0;
}
```

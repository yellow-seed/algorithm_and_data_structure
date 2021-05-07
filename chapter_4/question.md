4.2

```
#include <bits/stdc++.h>
using namespace std;

int top, S[1000];

void Push(int x) {
  S[++top] = x;
}

int Pop(){
  top--;
  return S[top + 1];
}

int main() {
  int a, b;
  top = 0;
  char s[100];
  
  while(scanf("%s", s) != EOF) {
    if(s[0] == '+'){
      a = Pop();
      b = Pop();
      Push(a + b);
    }else if(s[0] == '-'){
      a = Pop();
      b = Pop();
      Push(b - a);
    }else if(s[0] == '*'){
      a = Pop();
      b = Pop();
      Push(a * b);
    }else{
      int i = atoi(s);
      Push(i);
    }
  }

  cout << Pop() << endl;

  return 0;
}
```

4.3

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 1000000;

struct process {
  string name;
  int time;
};

process Q[MAX];
int tail = 0, head = 0;

bool isEmpty(){
  return (head == tail);
}

bool isFull(){
  return (head == (tail + 1) % MAX);
}

void enqueue(process v){
  if(isFull()){
    cout << "queue is full." << endl;
    return;
  }
  Q[tail++] = v;
  if(tail == MAX) tail = 0;
}

process dequeue(){
  if(isEmpty()){
    process p = {"", -1};
    cout << "queue is empty." << endl;
    return p;
  }
  process res = Q[head];
  ++head;
  if(head == MAX) head = 0;
  return res;
}

int main() {
  int n, q;
  int elaps =  0;
  cin >> n >> q;

  head = 0;
  tail = n + 1;

  vector<string> name(n);
  vector<int> time(n);

  for(int i = 0; i < n; i++){
    cin >> Q[i].name >> Q[i].time;
  }

  while(head != tail){
    process u = dequeue();
    int c = min(q, u.time);
    u.time -= c;
    elaps += c;
    if (u.time > 0){
      enqueue(u);
    } else {
      cout << u.name << " " << elaps << endl;
    }
  }


  return 0;
}
```

4.4

```
#include <bits/stdc++.h>
using namespace std;

struct Node {
  int key;
  Node *next, *prev;
};

Node *nil;

Node* listSearch(int key){
  Node *cur = nil->next;
  while (cur != nil && cur->key != key){
    cur = cur->next;
  }
  return cur;
}

void init(){
  nil = (Node *)malloc(sizeof(Node));
  nil->next = nil;
  nil->prev = nil;
}

void printList(){
  Node *cur = nil->next;
  int isf = 0;
  while(true){
    if(cur == nil) break;
    if(isf++ > 0) cout << " ";
    cout << cur->key;
    cur = cur->next;
  }
  cout << endl;
}

void deleteNode(Node *t){
  if(t == nil) return;
  t->prev->next = t->next;
  t->next->prev = t->prev;
  free(t);
}

void deleteFirst(){
  deleteNode(nil->next);
}

void deleteLast(){
  deleteNode(nil->prev);
}

void deleteKey(int key){
  deleteNode(listSearch(key));
}

void insert(int key){
  Node *x = (Node *)malloc(sizeof(Node));
  x->key = key;
  x->next = nil->next;
  nil->next->prev = x;
  nil->next = x;
  x->prev = nil;
}

int main() {
  int key, n, i;
  int size = 0;
  string command;
  int np = 0, nd = 0;
  cin >> n;

  init();

  for(int i = 0; i < n; i++){
    cin >> command >> key;
    if (command[0] == 'i'){
      insert(key);
      np++;
      size++;
    } else if(command[0] == 'd'){
      if (command.size() > 6){
        if(command[6] == 'F'){
          deleteFirst();
        }else if(command[6] == 'L'){
          deleteLast();
        }
      } else {
        deleteKey(key);
        nd++;
      }
      size--;
    }
  }

  printList();


  return 0;
}
```

4.6

```
```


9.2

```
#include <bits/stdc++.h>
using namespace std;

struct Node{
  int key;
  Node *parent, *left, *right;
};

Node *NIL, *root;

void insert(int key){
  Node *x, *y, *z;
  z = new Node;
  z->key = key;
  z->left = NIL;
  z->right = NIL;

  y = NIL;
  x = root;

  while(x != NIL){
    y = x;
    if(z->key < x->key){
      x = x->left;
    }else{
      x = x->right;
    }
  }

  z->parent = y;

  if(y == NIL){
    root = z;
  }else{
    if(z->key < y->key){
      y->left = z;
    }else{
      y->right = z;
    }
  }
}

void preOrderParse(Node *node){
  if(node == NIL)return;
  cout << node->key << " ";
  preOrderParse(node->left);
  preOrderParse(node->right);
}

void inOrderParse(Node *node){
  if(node == NIL)return;
  inOrderParse(node->left);
  cout << node->key << " ";
  inOrderParse(node->right);
}

int main() {
  int n;
  string com;
  int key;
  cin >> n;

  for(int i = 0; i < n; ++i){
    cin >> com;
    if(com == "insert"){
      cin >> key;
      insert(key);
    }else if(com == "print"){
      inOrderParse(root);
      cout << endl;
      preOrderParse(root);
      cout << endl;
    }
  }
  
  return 0;
}
```

9.3

```
#include <bits/stdc++.h>
using namespace std;

struct Node{
  int key;
  Node *parent, *left, *right;
};

Node *NIL, *root;

void insert(int key){
  Node *x, *y, *z;
  z = new Node;
  z->key = key;
  z->left = NIL;
  z->right = NIL;

  y = NIL;
  x = root;

  while(x != NIL){
    y = x;
    if(z->key < x->key){
      x = x->left;
    }else{
      x = x->right;
    }
  }

  z->parent = y;

  if(y == NIL){
    root = z;
  }else{
    if(z->key < y->key){
      y->left = z;
    }else{
      y->right = z;
    }
  }
}

Node* find(Node *node, int key){
  while(node != NIL && key != node->key){
    if(key < node->key){
      node = node->left;
    }else{
      node = node->right;
    }
  }
  return node;
}

void preOrderParse(Node *node){
  if(node == NIL)return;
  cout << node->key << " ";
  preOrderParse(node->left);
  preOrderParse(node->right);
}

void inOrderParse(Node *node){
  if(node == NIL)return;
  inOrderParse(node->left);
  cout << node->key << " ";
  inOrderParse(node->right);
}

int main() {
  int n;
  string com;
  int key;
  cin >> n;

  for(int i = 0; i < n; ++i){
    cin >> com;
    if(com == "find"){
      cin >> key;
      Node *target = find(root, key);
      if(target != NIL)cout << "yes" << endl;
      else cout << "no" << endl;
    }else if(com == "insert"){
      cin >> key;
      insert(key);
    }else if(com == "print"){
      inOrderParse(root);
      cout << endl;
      preOrderParse(root);
      cout << endl;
    }
  }
  
  return 0;
}
```

9.4

```
#include <bits/stdc++.h>
using namespace std;

struct Node{
  int key;
  Node *parent, *left, *right;
};

Node *NIL, *root;

void insert(int key){
  Node *x, *y, *z;
  z = new Node;
  z->key = key;
  z->left = NIL;
  z->right = NIL;

  y = NIL;
  x = root;

  while(x != NIL){
    y = x;
    if(z->key < x->key){
      x = x->left;
    }else{
      x = x->right;
    }
  }

  z->parent = y;

  if(y == NIL){
    root = z;
  }else{
    if(z->key < y->key){
      y->left = z;
    }else{
      y->right = z;
    }
  }
}

Node* find(int key){
  Node *node;
  node = root;
  while(node != NIL && key != node->key){
    if(key < node->key){
      node = node->left;
    }else{
      node = node->right;
    }
  }
  return node;
}

Node* next_node(Node *node){
  Node *x;

  if(node->right != NIL){
    x = x->right;
    while(x->left != NIL){
      x = x->left;
    }
  }else{
    x = node;
    while(x->parent != NIL && x == x->parent->right){
      x = x->parent;
    }
    x = x->parent;
  }
  return x;
}

void deleteNode(int key){
  Node *x, *y, *z;
  z = find(key);

  if(z->left == NIL || z->right == NIL){
    y = z;
  }else{
    y = next_node(z);
  }

  if(y->left != NIL)x = y->left;
  else x = y->right;

  if(x != NIL) x->parent = y->parent;
  if(y->parent == NIL){
    root = x;
  }else if(y == y->parent->left){
    y->parent->left = x;
  }else{
    y->parent->right = x;
  }

  if(z != y)z->key = y->key;

  delete y;
}

void preOrderParse(Node *node){
  if(node == NIL)return;
  cout << node->key << " ";
  preOrderParse(node->left);
  preOrderParse(node->right);
}

void inOrderParse(Node *node){
  if(node == NIL)return;
  inOrderParse(node->left);
  cout << node->key << " ";
  inOrderParse(node->right);
}

int main() {
  int n;
  string com;
  int key;
  cin >> n;

  for(int i = 0; i < n; ++i){
    cin >> com;
    if(com == "find"){
      cin >> key;
      Node *target = find(key);
      if(target != NIL)cout << "yes" << endl;
      else cout << "no" << endl;
    }else if(com == "insert"){
      cin >> key;
      insert(key);
    }else if(com == "print"){
      inOrderParse(root);
      cout << endl;
      preOrderParse(root);
      cout << endl;
    }else if(com == "delete"){
      cin >> key;
      deleteNode(key);
    }
  }
  
  return 0;
}
```
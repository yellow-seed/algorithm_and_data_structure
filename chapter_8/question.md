8.2

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100005;
const int NIL = -1;

struct Node{
  int parent, left, right;
};

Node gNode[MAX];
int gDepth[MAX];

void print(int node){
  //
  cout << "node" << node << ": ";
  cout << "parent" << gNode[node].parent << ", ";
  cout << "depth" << gDepth[node] << ", ";

  if(gNode[node].parent == NIL){cout << "root, ";}
  else if(gNode[node].left == NIL){cout << "leaf, ";}
  else {cout << "internal node, ";}

  cout << "[";

  for(int i = 0,left = gNode[node].left;left != NIL;++i,left = gNode[left].right){
    if(i){cout << ", ";}
    cout << left;
  }

  cout << "]" << endl;
}

void rec(int node, int parent){
  //
  gDepth[node] = parent;
  if(gNode[node].right != NIL){
    rec(gNode[node].right, parent);
  }

  if(gNode[node].left != NIL){
    rec(gNode[node].left, parent + 1);
  }
}

int main() {
  int n;
  int nodeNum, nodeIndex, node, left, root;
  cin >> n;

  for(int i = 0; i < n; ++i){
    gNode[i].parent = gNode[i].left = gNode[i].right = NIL;
  }

  for(int i = 0; i < n; ++i){
    cin >> nodeIndex >> nodeNum;
    for(int j = 0; j < nodeNum; ++j){
      //
      cin >> node;

      if(j == 0){
        //
        gNode[nodeIndex].left = node;
      } else {
        gNode[left].right = node;
      }
      left = node;
      gNode[node].parent = nodeIndex;
    }
  }

  for(int i = 0; i < n; ++i){
    if(gNode[i].parent == NIL){root = i;}
  }

  rec(root, 0);

  for(int i = 0; i < n; ++i){
    print(i);
  }
  
  return 0;
}
```

8.3

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100005;
const int NIL = -1;

struct Node{
  int parent, left, right;
};

Node gNode[MAX];
int gDepth[MAX], gHeight[MAX];

void setDepth(int node, int depth){
  if(node == NIL)return;
  gDepth[node] = depth;
  setDepth(gNode[node].left, depth + 1);
  setDepth(gNode[node].right, depth + 1);
}

int setHeight(int node){
  int leftHeight = 0, rightHeight = 0;
  if(gNode[node].left != NIL){
    leftHeight = setHeight(gNode[node].left) + 1;
  }
  if(gNode[node].right != NIL){
    rightHeight = setHeight(gNode[node].right) + 1;
  }
  return gHeight[node] = (leftHeight > rightHeight ? leftHeight : rightHeight);
}

int getSibiling(int node){
  if(gNode[node].parent == NIL)return NIL;
  if(gNode[gNode[node].parent].left != node && gNode[gNode[node].parent].left != NIL){
    return gNode[gNode[node].parent].left;
  }
  if(gNode[gNode[node].parent].right != node && gNode[gNode[node].parent].right != NIL){
    return gNode[gNode[node].parent].right;
  }
  return NIL;
}

void print(int node){
  cout << "node " << node << ": ";
  cout << "parent = " << gNode[node].parent << ", ";
  cout << "sibiling = " << getSibiling(node) << ", ";

  int deg = 0;
  if(gNode[node].left != NIL) deg++;
  if(gNode[node].right != NIL) deg++;

  cout << "degree = " << deg << ", ";
  cout << "depth = " << gDepth[node] << ", ";
  cout << "height = " << gHeight[node] << ", ";

  if(gNode[node].parent == NIL){
    cout << "root";
  } else if(gNode[node].left == NIL && gNode[node].right == NIL){
    cout << "leaf";
  } else {
    cout << "internal node";
  }
  cout << endl;
}

int main() {
  int n;
  int nodeIndex, left, right, root;
  cin >> n;

  for(int i = 0; i < n; ++i){
    gNode[i].parent = gNode[i].left = gNode[i].right = NIL;
  }

  for(int i = 0; i < n; ++i){
    cin >> nodeIndex >> left >> right;
    gNode[nodeIndex].left = left;
    gNode[nodeIndex].right = right;
    if(left != NIL)gNode[left].parent = nodeIndex;
    if(right != NIL)gNode[right].parent = nodeIndex;
  }

  for(int i = 0; i < n; ++i){
    if(gNode[i].parent == NIL)root = i;
  }

  setDepth(root, 0);
  setHeight(root);

  for(int i = 0; i < n; ++i)print(i);
  
  return 0;
}
```

8.4

```
#include <bits/stdc++.h>
using namespace std;
const int MAX = 100005;
const int NIL = -1;

struct Node{
  int parent, left, right;
};

Node gNode[MAX];

void preOrderParse(int node){
  if(node == NIL)return;
  cout << node << " ";
  preOrderParse(gNode[node].left);
  preOrderParse(gNode[node].right);
}

void inOrderParse(int node){
  if(node == NIL)return;
  inOrderParse(gNode[node].left);
  cout << node << " ";
  inOrderParse(gNode[node].right);
}

void postOrderParse(int node){
  if(node == NIL)return;
  postOrderParse(gNode[node].left);
  postOrderParse(gNode[node].right);
  cout << node << " ";
}

int main() {
  int n;
  int nodeIndex, left, right, root;
  cin >> n;

  for(int i = 0; i < n; ++i)gNode[i].parent = NIL;

  for(int i = 0; i < n; ++i){
    cin >> nodeIndex >> left >> right;
    gNode[nodeIndex].left = left;
    gNode[nodeIndex].right = right;
    if(left != NIL)gNode[left].parent = nodeIndex;
    if(right != NIL)gNode[right].parent = nodeIndex;
  }

  for(int i = 0; i < n; ++i){
    if(gNode[i].parent == NIL)root = i;
  }

  cout << "Preorder" << endl;
  preOrderParse(root);
  cout << endl;

  cout << "Inorder" << endl;
  inOrderParse(root);
  cout << endl;

  cout << "Postorder" << endl;
  postOrderParse(root);
  cout << endl;
  
  return 0;
}
```

8.5

```
```
16.2

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

class Point {
  public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

struct Segment{
  Point p1, p2;
};

typedef Point Vector;
typedef Segment Line;

double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x*b.y - a.y*b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

int main() {
  int n;
  cin >> n;

  vector<vector<Point>> p(n, vector<Point>(4));

  for(int i = 0; i < n; i++){
    for(int j = 0; j < 4; j++){
      cin >> p[i][j].x >> p[i][j].y;
    }
  }

  for(int i = 0; i < n; i++){
    Point p0 = p[i][0];
    Point p1 = p[i][1];
    Point p2 = p[i][2];
    Point p3 = p[i][3];

    Vector a = p1 - p0;
    Vector b = p3 - p2;
    if(isPararel(a, b)){
      cout << 2 << endl;
    }else if(isOrthogonal(a, b)){
      cout << 1 << endl;
    }else{
      cout << 0 << endl;
    }
  }

  return 0;
}
```

16.3

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

class Point {
  public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

struct Segment{
  Point p1, p2;
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

int main() {
  Point p1, p2;
  cin >> p1.x >> p1.y >> p2.x >> p2.y;
  Segment s(p1, p2);

  int q;
  cin >> q;
  vector<Point> pp(q);
  for(int i = 0; i < q; i++){
    cin >> pp[i].x >> pp[i].y;
  }

  for(int i = 0; i < q; i++){
    Point ans = project(s, pp[i]);
    cout << ans.x << " " << ans.y <<endl;
  }


  return 0;
}
```

16.4

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

class Point {
  public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

struct Segment{
  Point p1, p2;
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

int main() {
  Point p1, p2;
  cin >> p1.x >> p1.y >> p2.x >> p2.y;
  Segment s(p1, p2);

  int q;
  cin >> q;
  vector<Point> pp(q);
  for(int i = 0; i < q; i++){
    cin >> pp[i].x >> pp[i].y;
  }

  for(int i = 0; i < q; i++){
    Point ans = reflect(s, pp[i]);
    cout << ans.x << " " << ans.y <<endl;
  }


  return 0;
}
```

16.5

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
  public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

int main() {
  int q;
  cin >> q;

  for(int i = 0; i < q; i++){
    Segment s1, s2;
    cin >> s1.p1.x >> s1.p1.y >> s1.p2.x >> s1.p2.y;
    cin >> s2.p1.x >> s2.p1.y >> s2.p2.x >> s2.p2.y;

    cout << getDistance(s1, s2) << endl;
  }

  return 0;
}
```

16.6

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
  public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

int main() {
  Point p0, p1;
  cin >> p0.x >> p0.y >> p1.x >> p1.y;

  int q;
  cin >> q;

  for(int i = 0; i < q; i++){
    Point p;
    cin >> p.x >> p.y;
    int ans = ccw(p0, p1, p);
    if(ans == COUNTER_CLOCKWISE) cout << "COUNTER_CLOCKWISE" << endl;
    else if(ans == CLOCKWISE) cout << "CLOCKWISE" << endl;
    else if(ans == ONLINE_BACK) cout << "ONLINE_BACK" << endl;
    else if(ans == ON_SEGMENT) cout << "ON_SEGMENT" << endl;
    else if(ans == ONLINE_FRONT) cout << "ONLINE_FRONT" << endl;
  }

  return 0;
}
```

16.7

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
  public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

int main() {
  int q;
  cin >> q;

  for(int i = 0; i < q; i++){
    Point p0, p1, p2, p3;
    cin >> p0.x >> p0.y >> p1.x >> p1.y >> p2.x >> p2.y >> p3.x >> p3.y;
    Segment s1(p0, p1), s2(p2, p3);

    if(intersect(s1, s2)){
      cout << 1 << endl;
    }else{
      cout << 0 << endl;
    }
  }

  return 0;
}
```

16.8

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
  public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

Point getCrossPoint(Segment s1, Segment s2){
  Vector base = s2.p2 - s2.p1;
  double d1 = abs(cross(base, s1.p1 - s2.p1));
  double d2 = abs(cross(base, s1.p2 - s2.p2));
  double t = d1 / (d1 + d2);
  return s1.p1 + (s1.p2 - s1.p1) * t;
}

int main() {
  int q;
  cin >> q;

  for(int i = 0; i < q; i++){
    Point p0, p1, p2, p3;
    cin >> p0.x >> p0.y >> p1.x >> p1.y >> p2.x >> p2.y >> p3.x >> p3.y;
    Segment s1(p0, p1), s2(p2, p3);

    Point ans = getCrossPoint(s1, s2);
    cout << ans.x << " " << ans.y << endl;
  }

  return 0;
}
```

16.9

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

class Circle{
public:
  Point c;
  double r;
  Circle(Point c = Point(), double r = 0.0): c(c), r(r){}
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;
typedef vector<Point> Polygon;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

Point getCrossPoint(Segment s1, Segment s2){
  Vector base = s2.p2 - s2.p1;
  double d1 = abs(cross(base, s1.p1 - s2.p1));
  double d2 = abs(cross(base, s1.p2 - s2.p2));
  double t = d1 / (d1 + d2);
  return s1.p1 + (s1.p2 - s1.p1) * t;
}

pair<Point, Point> getCrossPoints(Circle c, Line l){
  Vector pr = project(l, c.c);
  Vector e = (l.p2 - l.p1) / abs(l.p2 - l.p1);
  double base = sqrt(c.r * c.r - norm(pr - c.c));
  return make_pair(pr + e * base, pr - e * base);
}

int main() {
  Circle c;
  int q;
  cin >> c.c.x >> c.c.y >> c.r;
  cin >> q;

  vector<Line> l(q);
  for(int i = 0; i < q; i++){
    cin >> l[i].p1.x >> l[i].p1.y >> l[i].p2.x >> l[i].p2.y;
  }

  for(int i = 0; i < q; i++){
    pair<Point, Point> p = getCrossPoints(c, l[i]);
    if(p.second.x == p.first.x){
      if(p.first.y < p.second.y) cout << p.first.x << " " << p.first.y << " " << p.second.x << " " << p.second.y << endl;
      else cout << p.second.x << " " << p.second.y << " " << p.first.x << " " << p.first.y << endl;
    }else{
      cout << p.second.x << " " << p.second.y << p.first.x << " " << p.first.y << endl;
    }
  }

  return 0;
}
```

16.10

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

class Circle{
public:
  Point c;
  double r;
  Circle(Point c = Point(), double r = 0.0): c(c), r(r){}
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;
typedef vector<Point> Polygon;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}
double arg(Vector a){return atan2(a.y, a.x);}
Vector polar(double a, double r){return Point(cos(r) * a, sin(r) * a);}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

Point getCrossPoint(Segment s1, Segment s2){
  Vector base = s2.p2 - s2.p1;
  double d1 = abs(cross(base, s1.p1 - s2.p1));
  double d2 = abs(cross(base, s1.p2 - s2.p2));
  double t = d1 / (d1 + d2);
  return s1.p1 + (s1.p2 - s1.p1) * t;
}

pair<Point, Point> getCrossPoints(Circle c, Line l){
  Vector pr = project(l, c.c);
  Vector e = (l.p2 - l.p1) / abs(l.p2 - l.p1);
  double base = sqrt(c.r * c.r - norm(pr - c.c));
  return make_pair(pr + e * base, pr - e * base);
}

pair<Point, Point> getCrossPoints(Circle c1, Circle c2){
  double d = abs(c1.c - c2.c);
  double a = acos((c1.r * c1.r + d * d - c2.r * c2.r) / (2 * c1.r * d));
  double t = arg(c2.c - c1.c);
  return make_pair(c1.c + polar(c1.r, t + a), c1.c + polar(c1.r, t - a));
}

int main() {
  Circle c1, c2;
  cin >> c1.c.x >> c1.c.y >> c1.r;
  cin >> c2.c.x >> c2.c.y >> c2.r;

  pair<Point, Point> p = getCrossPoints(c1, c2);
  if(p.first.x == p.second.x){
    if(p.first.y < p.second.y) cout << p.first.x << " " << p.first.y << " " << p.second.x << " " << p.second.y << endl;
    else cout << p.second.x << " " << p.second.y << " " << p.first.x << " " << p.first.y << endl;
  }else if(p.first.x < p.second.x){
    cout << p.first.x << " " << p.first.y << " " << p.second.x << " " << p.second.y << endl;
  }else{
    cout << p.second.x << " " << p.second.y << " " << p.first.x << " " << p.first.y << endl;
  }

  return 0;
}
```

16.11

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

class Circle{
public:
  Point c;
  double r;
  Circle(Point c = Point(), double r = 0.0): c(c), r(r){}
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;
typedef vector<Point> Polygon;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}
double arg(Vector a){return atan2(a.y, a.x);}
Vector polar(double a, double r){return Point(cos(r) * a, sin(r) * a);}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

int contains(Polygon g, Point p){
  int n = g.size();
  bool x = false;
  for(int i = 0; i < n; i++){
    Point a = g[i] - p;
    Point b = g[(i + 1) % n] - p;
    if(abs(cross(a, b)) < DBL_EPSILON && dot(a, b) < DBL_EPSILON) return 1;
    if(a.y > b.y) swap(a, b);
    if(a.y < DBL_EPSILON && DBL_EPSILON < b.y && DBL_EPSILON && cross(a, b) > DBL_EPSILON) x = !x;
  }
  return (x ? 2 : 0);
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

Point getCrossPoint(Segment s1, Segment s2){
  Vector base = s2.p2 - s2.p1;
  double d1 = abs(cross(base, s1.p1 - s2.p1));
  double d2 = abs(cross(base, s1.p2 - s2.p2));
  double t = d1 / (d1 + d2);
  return s1.p1 + (s1.p2 - s1.p1) * t;
}

pair<Point, Point> getCrossPoints(Circle c, Line l){
  Vector pr = project(l, c.c);
  Vector e = (l.p2 - l.p1) / abs(l.p2 - l.p1);
  double base = sqrt(c.r * c.r - norm(pr - c.c));
  return make_pair(pr + e * base, pr - e * base);
}

pair<Point, Point> getCrossPoints(Circle c1, Circle c2){
  double d = abs(c1.c - c2.c);
  double a = acos((c1.r * c1.r + d * d - c2.r * c2.r) / (2 * c1.r * d));
  double t = arg(c2.c - c1.c);
  return make_pair(c1.c + polar(c1.r, t + a), c1.c + polar(c1.r, t - a));
}

int main() {
  int n;
  cin >> n;
  Polygon pg(n);

  for(int i = 0; i < n; i++){
    Point p;
    cin >> p.x >> p.y;
    pg[i] = p;
  }

  int q;
  cin >> q;

  for(int i = 0; i < q; i++){
    Point p;
    cin >> p.x >> p.y;

    cout << contains(pg, p) << endl;
  }

  return 0;
}
```

16.12

```
#include <bits/stdc++.h>
using namespace std;

#define equals(a, b) (fabs((a) - (b)) < DBL_EPSILON)

static const int COUNTER_CLOCKWISE = 1;
static const int CLOCKWISE = -1;
static const int ONLINE_BACK = 2;
static const int ONLINE_FRONT = -2;
static const int ON_SEGMENT = 0;

class Point {
public:
  double x, y;

  Point(double x = 0, double y = 0): x(x), y(y){}
  
  Point operator + (Point p){return Point(x + p.x, y + p.y);}
  Point operator - (Point p){return Point(x - p.x, y - p.y);}
  Point operator * (double a){return Point(a * x, a * y);}
  Point operator / (double a){return Point(x / a, y / a);}

  double abs(){return sqrt(norm());}
  double norm(){return x * x + y * y;}

  bool operator < (const Point &p) const {
    return x != p.x ? x < p.x : y < p.y;
  }

  bool operator == (const Point &p) const {
    return fabs(x - p.x) < DBL_EPSILON && fabs(y - p.y) < DBL_EPSILON;
  }
};

class Circle{
public:
  Point c;
  double r;
  Circle(Point c = Point(), double r = 0.0): c(c), r(r){}
};

struct Segment{
  Point p1, p2;
  Segment(){}
  Segment(Point p1, Point p2): p1(p1), p2(p2){}
};

typedef Point Vector;
typedef Segment Line;
typedef vector<Point> Polygon;

double norm(Vector a){return a.x * a.x + a.y * a.y;}
double abs(Vector a){return sqrt(norm(a));}
double dot(Vector a, Vector b){return a.x * b.x + a.y * b.y;}
double cross(Vector a, Vector b){return a.x * b.y - a.y * b.x;}
double arg(Vector a){return atan2(a.y, a.x);}
Vector polar(double a, double r){return Point(cos(r) * a, sin(r) * a);}

bool isOrthogonal(Vector a, Vector b){
  return equals(dot(a, b), 0.0);
}

bool isOrthogonal(Point a1, Point a2, Point b1, Point b2){
  return isOrthogonal(a1 - a2, b1 - b2);
}

bool isOrthogonal(Segment s1, Segment s2){
  return equals(dot(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

bool isPararel(Vector a, Vector b){
  return equals(cross(a, b), 0.0);
}

bool isPararel(Point a1, Point a2, Point b1, Point b2){
  return isPararel(a1 - a2, b1 - b2);
}

bool isPararel(Segment s1, Segment s2){
  return equals(cross(s1.p2 - s1.p1, s2.p2 - s2.p1), 0.0);
}

int ccw(Point p0, Point p1, Point p2){
  Vector a = p1 - p0;
  Vector b = p2 - p0;
  if(cross(a, b) > DBL_EPSILON) return COUNTER_CLOCKWISE;
  if(cross(a, b) < -DBL_EPSILON) return CLOCKWISE;
  if(dot(a, b) < -DBL_EPSILON) return ONLINE_BACK;
  if(a.norm() < b.norm()) return ONLINE_FRONT;

  return ON_SEGMENT;
}

int contains(Polygon g, Point p){
  int n = g.size();
  bool x = false;
  for(int i = 0; i < n; i++){
    Point a = g[i] - p;
    Point b = g[(i + 1) % n] - p;
    if(abs(cross(a, b)) < DBL_EPSILON && dot(a, b) < DBL_EPSILON) return 1;
    if(a.y > b.y) swap(a, b);
    if(a.y < DBL_EPSILON && DBL_EPSILON < b.y && DBL_EPSILON && cross(a, b) > DBL_EPSILON) x = !x;
  }
  return (x ? 2 : 0);
}

bool intersect(Point p1, Point p2, Point p3, Point p4){
  return (ccw(p1, p2, p3) * ccw(p1, p2, p4) <= 0 && ccw(p3, p4, p1) * ccw(p3, p4, p2) <= 0);
}

bool intersect(Segment s1, Segment s2){
  return intersect(s1.p1, s1.p2, s2.p1, s2.p2);
}

double getDistance(Point a, Point b){
  return abs(a - b);
}

double getDistanceLP(Line l, Point p){
  return abs(cross(l.p2 - l.p1, p - l.p1) / abs(l.p2 - l.p1));
}

double getDistanceSP(Segment s, Point p){
  if(dot(s.p2 - s.p1, p - s.p1) < 0.0) return abs(p - s.p1);
  if(dot(s.p1 - s.p2, p - s.p2) < 0.0) return abs(p - s.p2);
  return getDistanceLP(s, p);
}

double getDistance(Segment s1, Segment s2){
  if(intersect(s1, s2)) return 0.0;
  return min(min(getDistanceSP(s1, s2.p1), getDistanceSP(s1, s2.p2)), min(getDistanceSP(s2, s1.p1), getDistanceSP(s2, s1.p2)));
}

Point project(Segment s, Point p){
  Vector base = s.p2 - s.p1;
  double r = dot(p - s.p1, base) / norm(base);
  return s.p1 + base * r;
}

Point reflect(Segment s, Point p){
  return p + (project(s, p) - p) * 2.0;
}

Point getCrossPoint(Segment s1, Segment s2){
  Vector base = s2.p2 - s2.p1;
  double d1 = abs(cross(base, s1.p1 - s2.p1));
  double d2 = abs(cross(base, s1.p2 - s2.p2));
  double t = d1 / (d1 + d2);
  return s1.p1 + (s1.p2 - s1.p1) * t;
}

pair<Point, Point> getCrossPoints(Circle c, Line l){
  Vector pr = project(l, c.c);
  Vector e = (l.p2 - l.p1) / abs(l.p2 - l.p1);
  double base = sqrt(c.r * c.r - norm(pr - c.c));
  return make_pair(pr + e * base, pr - e * base);
}

pair<Point, Point> getCrossPoints(Circle c1, Circle c2){
  double d = abs(c1.c - c2.c);
  double a = acos((c1.r * c1.r + d * d - c2.r * c2.r) / (2 * c1.r * d));
  double t = arg(c2.c - c1.c);
  return make_pair(c1.c + polar(c1.r, t + a), c1.c + polar(c1.r, t - a));
}

Polygon andrewScan(Polygon s){
  Polygon u, l;
  if(s.size() < 3) return s;
  sort(s.begin(), s.end());

  u.push_back(s[0]);
  u.push_back(s[1]);

  l.push_back(s[s.size() - 1]);
  l.push_back(s[s.size() - 2]);

  //上側
  for(int i = 2; i < s.size(); i++){
    for(int n = u.size(); n >= 2 && ccw(u[n - 2], u[n - 1], s[i]) == COUNTER_CLOCKWISE; n--){
      u.pop_back();
    }
    u.push_back(s[i]);
  }

  //下側
  for(int i = s.size() - 3; i >= 0; i--){
    for(int n = l.size(); n >= 2 && ccw(l[n - 2], l[n - 1], s[i]) == COUNTER_CLOCKWISE; n--){
      l.pop_back();
    }
    l.push_back(s[i]);
  }

  reverse(l.begin(), l.end());
  for(int i = u.size() - 2; i >= 1; i--) l.push_back(u[i]);

  return l;
}

int main() {
  int n;
  cin >> n;

  vector<Point> p(n);
  for(int i = 0; i < n; i++){
    cin >> p[i].x >> p[i].y;
  }

  Polygon pp = andrewScan(p);

  cout << pp.size() << endl;
  for(int i = 0; i < pp.size(); i++) cout << pp[i].x << " " << pp[i].y << endl;

  return 0;
}
```

16.13

```
```
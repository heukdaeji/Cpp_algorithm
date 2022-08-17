# 개미 [백준 10158번](https://www.acmicpc.net/problem/10158)

## 문제 접근
* 일단 x좌표만 생각해보자.
* 일단 개미가 계산하기 편리하게 0까지 보내면 시간은 (w+(w-p))시간이 걸린다.
* 이 중에 p+t, 즉 도착한 위치가 0까지 도달하지 못 할시를 대비해 예외 방지 코드를 생각한다.
* 이제 기존 t에서 저 값을 뺀 값을 2w로 나눈 나머지를 생각하면 값이 나온다.
* 만약 2w로 나눈 나머지가 w보다 크다면 시간이 지났을 때 0으로 가는 쪽에 있을 것이고 아니면 w쪽으로 가고 있을 것이다.
* 이런 식으로 y좌표도 값을 구해주면 된다.

```cpp
#include <iostream>

using namespace std;

int w, h, p, q, t;
int ansx, ansy;

int main() {
    cin >> w >> h;
    cin >> p >> q;
    cin >> t;
    if (p+t <= w) ansx = p+t;
    else if (w < (p+t) && p+t <= 2*w) ansx = 2*w-p-t;
    else if ((t-(2*w-p)) % (2*w) <= w) ansx = (t-(2*w-p)) % (2*w);
    else ansx = 2*w - ((t-(2*w-p)) % (2*w));
    if (q+t <= h) ansy = q+t;
    else if (h < q+t && q+t < 2*h) ansy = 2*h-q-t;
    else if ((t-(2*h-q)) % (2*h) <= h) ansy = (t-(2*h-q)) % (2*h);
    else ansy = 2*h - ((t-(2*h-q)) % (2*h));
    cout << ansx << " " << ansy;
}

```

# 가로수 [백준 2485번](https://www.acmicpc.net/problem/2485)
```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> tree;

int gcd(int a, int b) {
    if (a == 0) return b;
    else if (b == 0) return a;
    else {
        if (a > b) {
            return gcd(b, a % b);
        }
        else {
            return gcd(a, b % a);
        }
    }
}

int N, x;

int main() {
    cin >> N;
    for (int i = 0; i < N; i++) {
        cin >> x;
        tree.push_back(x);
    }
    int G = tree[1] - tree[0];
    for (int i = 1; i < N-1; i++) {
        G = gcd(tree[i+1] - tree[i], G);
    }
    cout << ((tree[N-1] - tree[0]) / G) - (tree.size() - 1);
}
```

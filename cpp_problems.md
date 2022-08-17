# 개미 [백준 10158번](https://www.acmicpc.net/problem/10158)

## 문제 접근
* 일단 x좌표만 생각해보자.
* 일단 개미가 계산하기 편리하게 0까지 보내면 시간은 (w+(w-p))시간이 걸린다.
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
    else if ((t-(2*w-p)) % 2*w <= w) ansx = (t-(2*w-p)) % (2*w);
    else ansx = w - ((t-(2*w-p)) % (2*w));
    if (q+t <= h) ansy = q+t;
    if ((t-(2*h-q)) % 2*h <= h) ansy = t-(2*h-q) % (2*h);
    else ansy = h - ((t-(2*h-q)) % (2*h));
    cout << ansx << " " << ansy;
}
```

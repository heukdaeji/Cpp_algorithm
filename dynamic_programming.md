# 369 게임

[10802번](https://www.acmicpc.net/problem/10802)

## 문제 접근
* ~~

* 알고리즘: 다이나믹 프로그래밍, 자료구조: ~\~, 시간복잡도: ~\~

## 어려웠던 점
* ~~

## 해결 방법
* ~~

## 핵심 코드

* ~~

# 계단오르기

[(2579)](https://www.acmicpc.net/problem/2579)

## 문제 접근
* i번째 점수를 a\[i], i번째까지의 점수 총합을 d\[i], 1번 연속: d\[i]\[0], 2번 연속: d\[i][1]이라 하면,
* d\[i]\[0] = max(d\[i-2]\[0], d\[i-2]\[1]) + a\[i], d\[i]\[1] = d\[i-1]\[0] + a\[i];

* 알고리즘: DP

## 핵심 코드

``` cpp
    d[0][0] = d[0][1] = a[0];
    d[1][0] = a[0] + a[1];
    d[1][1] = a[1];
```
* 0번째 값과 1번째 값을 정해준다.
```cpp
    for (int i = 2; i < N; i++) {
        d[i][0] = d[i-1][1] + a[i];
        d[i][1] = max(d[i-2][0], d[i-2][1]) + a[i];
    }
```
* 각각의 1번 연속, 2번 연속 점수 총합을 구해준다.
## 소스 코드

```cpp
    #include <iostream>

    using namespace std;

    int a[301], d[301][2], N;

    int main() {
        cin >> N;
        for (int i = 0; i < N; i++) {
            cin >> a[i];
        }
        d[0][0] = d[0][1] = a[0];
        d[1][0] = a[0] + a[1];
        d[1][1] = a[1];
        for (int i = 2; i < N; i++) {
            d[i][0] = d[i-1][1] + a[i];
            d[i][1] = max(d[i-2][0], d[i-2][1]) + a[i];
        }
        cout << max(d[N-1][0], d[N-1][1]);
}
```

# 퇴사 

[(2579)](https://www.acmicpc.net/problem/2579)

## 문제 접근
* 일을 했을 때면, d\[(현재 날짜) + T]에 그때까지의 금액과 원래 금액의 max를 넣는다. 하지 않는다면, 그냥 넘어간다. 
* 다음 날에 들어있는 금액이 없거나 전날의 금액보다 작다면, 전 날의 금액으로 설정한다.
* 사용 알고리즘: DP

## 핵심 코드

```cpp
for (int i = 1; i <= N; i++) {
    d[i] = max(d[i], d[i-1]);
    if (T[i] + i <= N+1) {
        d[T[i] + i] = max(d[T[i] + i], d[i] + P[i]);
    }
}
d[N+1] = max(d[N], d[N+1]);
```
* d\[i]가 0일 경우가 있으므로  d\[i-1]과 비교한다.
* T\[i] + i가 기간 안이라면 d\[T\[i] + i]에 넣는데, 이때 안에 더 큰 값이 들어있을 경우 원래 (d\[T\[i] + i]와 비교한다.

## 소스 코드
```cpp
#include <iostream>
#include <algorithm>

using namespace std;

int N, d[17], T[16], P[16];

int main() {
    cin >> N;
    for (int i = 1; i <= N; i++) {
        cin >> T[i] >> P[i];
    }
    d[0] = 0;
    for (int i = 1; i <= N; i++) {
        d[i] = max(d[i], d[i-1]);
        if (T[i] + i <= N+1) {
            d[T[i] + i] = max(d[T[i] + i], d[i] + P[i]);
        }
    }
    d[N+1] = max(d[N], d[N+1]);
    cout << d[N+1];
}
```

# 하노이 탑 이동순서(백준 11729번)

* 소스코드:
```cpp
#include <iostream>

using namespace std;

int N;

void Hanoi(int n, int x, int y) {
    if (n == 0) return;
    Hanoi(n-1, x, 6-x-y);
    cout << x << " " << y << "\n";
    Hanoi(n-1, 6-x-y, y);
}

int main() {
    cin >> N;
    cout << (1<<N)-1 << "\n";
    Hanoi(N, 1, 3);
}
```

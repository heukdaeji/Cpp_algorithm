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

# 종이의 개수

* 소스코드:
```cpp#include <iostream>
#include <algorithm>
#include <string>

using namespace std;

int N, A[64][64];

// 1: pos, 0: any, -1: neg

int Tpos = 0, Tany = 0, Tneg = 0;

void BiBinarySearch(int StartX, int StartY, int len) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            int pos = 0, any = 0, neg = 0;
            if (i == 0) int ylen = StartY;
            else if (i == 1) int ylen = len/3 + StartY;
            else int ylen = 2*len/3 + StartY;
            if (j == 0) int xlen = StartX;
            else if (j == 1) int xlen = len/3 + StartX;
            else int xlen = 2*len/3 + StartX;
            for (int k = ylen; k < ylen+(len/3); k++) {
                for (int l = xlen; l < xlen+(len/3); l++) {
                    if (A[k][l] == 1) pos++;
                    else if (A[k][l] == 0) any++;
                    else neg++;
                }
            }
            if (pos == (N/3)*(N/3)) cout << 1;
            else if (any == (N/3)*(N/3)) cout << 0;
            else if (neg == (N/3)*(N/3)) Tneg++;
            else {
                int sX, sY;
                if (i == 0) int sY = StartY;
                else if (i == 1) int sY = len/3 + StartY;
                else int sY = 2*len/3 + StartY;
                if (j == 0) int sX = StartX;
                else if (j == 1) int sX = len/3 + StartX;
                else int sX = 2*len/3 + StartX;
                BiBinarySearch(sX, sY, len/3);
            }
        }
    }
    return;
}

int main() {
    cin >> N;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cin >> A[i][j];
            if (A[i][j] == 1) pos++;
            else if (A[i][j] == 0) any++;
            else if (A[i][j] == -1) neg++;
        }
    }
    if (pos == N*N) Tpos++;
    else if (any == N*N) Tany++;
    else if (neg == N*N) Tneg++;
    else BiBinarySearch(0, 0, N);
    printf("%d\n%d\n%d\n", Tpos, Tany, Tneg);
}
```

# 종이의 개수

* 소스 코드:
```cpp
#include <iostream>
#include <algorithm>
#include <string>

using namespace std;

int N, A[2200][2200];

// 1: pos, 0: any, -1: neg

int Tpos = 0, Tany = 0, Tneg = 0;

void BiBinarySearch(int StartX, int StartY, int len) {
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            int pos = 0, any = 0, neg = 0, xlen, ylen;
            if (i == 0) ylen = StartY;
            else if (i == 1) ylen = len/3 + StartY;
            else ylen = 2*(len/3) + StartY;
            if (j == 0) xlen = StartX;
            else if (j == 1) xlen = len/3 + StartX;
            else xlen = 2*(len/3) + StartX;
            for (int k = ylen; k < ylen+(len/3); k++) {
                for (int l = xlen; l < xlen+(len/3); l++) {
                    if (A[k][l] == 1) pos++;
                    else if (A[k][l] == 0) any++;
                    else if (A[k][l] == -1) neg++;
                }
            }
            if (pos == (len/3)*(len/3)) {
                Tpos++;
                
            } else if (any == (len/3)*(len/3)) {
                Tany++;
            } else if (neg == (len/3)*(len/3)) {
                Tneg++;
                
            } else {
                int sX, sY;
                if (i == 0) sY = StartY;
                else if (i == 1) sY = len/3 + StartY;
                else sY = 2*(len/3) + StartY;
                if (j == 0) sX = StartX;
                else if (j == 1) sX = len/3 + StartX;
                else sX = 2*(len/3) + StartX;
                BiBinarySearch(sX, sY, len/3);
            }
        }
    }
    return;
}

int main() {
    cin >> N;
    int pos = 0, any = 0, neg = 0;
    for (int i = 0; i < N; i++) {
        for (int j = 0; j < N; j++) {
            cin >> A[i][j];
            if (A[i][j] == 1) pos++;
            else if (A[i][j] == 0) any++;
            else if (A[i][j] == -1) neg++;
        }
    }
    if (pos == N*N) Tpos++;
    else if (any == N*N) Tany++;
    else if (neg == N*N) Tneg++;
    else BiBinarySearch(0, 0, N);
    printf("%d\n%d\n%d\n", Tneg, Tany, Tpos);
}
```

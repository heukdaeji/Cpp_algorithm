# 부등호 [백준 2529번/https://www.acmicpc.net/problem/2529]

* 코드:
```cpp
#include <iostream>
#include <vector>
#include <cmath>
#include <string>

using namespace std;

bool used[10];
int bs[9];
int N;
vector<int> v;
vector<string> nums;

void dfs(int x, int t) {
    v.push_back(x);
    // for (int j = 0; j < t; j++) {
    //     cout << "L";
    // }
    // cout << x << "\n";
    if (t == N) {
        string ans = "";
        for (int j = 0; j <= N; j++) {
            ans += to_string(v[j]);
        }
        nums.push_back(ans);
        used[x] = false;
        v.pop_back();
        return;
    }
    used[x] = true;
    for (int j = 9; j >= 0; j--) {
        if (!used[j]) {
            if (bs[t] == 1 && x > j) dfs(j, t+1);
            else if (bs[t] == 0 && x < j) dfs(j, t+1);
        }
    }
    used[x] = false;
    v.pop_back();
    return;
    
}

int main() {
    cin >> N;
    char c;
    for (int i = 0; i < N; i++) {
        cin >> c;
        if (c == '>') bs[i] = 1;
        else if (c == '<') bs[i] = 0;
    }
    for (int i = 9; i >= 0; i--) {
        dfs(i, 0);
    }
    cout << nums[0] << "\n" << nums[nums.size()-1];
}
```

# 1074번 Z
* 코드:
```cpp
#include <iostream>
#include <algorithm>
#include <cmath>

using namespace std;

int N, r, c;

void BiBinarySearch(int StartX, int StartY, int len, int num) {
    if (len == 2) {
        for (int i = 0; i < 4; i++) {
            int ylen = (i < 2) ? StartY : (StartY + 1);
            int xlen = (i % 2 == 0) ? StartX : (StartX + 1);
            if (ylen == c && xlen == r) {
                cout << num+i;
                exit(0);
            }
        }
    }
    else {
        for (int i = 0; i < 4; i++) {
            int ylen = (i < 2) ? StartY : (StartY + len/2);
            int xlen = (i % 2 == 0) ? StartX : (StartX + len/2);
            BiBinarySearch(ylen, xlen, len/2, len*i+num);
        }
    }
    cout << num << ", end" << len << "\n";
}



int main() {
    cin >> N >> r >> c;
    BiBinarySearch(0, 0, pow(2, N), 0);
}
```

* 비밀번호 (백준 2464번)
* 소스 코드:

```cpp
#include <iostream>
#include <cmath>
#include <algorithm>

using namespace std;

int a[64], b[64], a_n = 0;
long long A, smallA, bigA;
int prev = 0, next = 0;

int TwoToTen() {
    for (int i = 0; i < 63; i++) {
        
    }
}

int main() {
    cin >> A;
    long long x;
    while (A > 0) {
        x = A % 2;
        A /= 2;
        a[a_n] = x;
        a_n++;
    }
    for (int i = 0; i < a_n; i++) {
        b[a_n-1-i] = a[i];
    }
    for (int i = 0; i < a_n; i++) {
        cout << b[i];
    }
    prev_permutation(b, b+a_n-1);
    
    next_permutation(b, b+a_n-1);
    next_permutation(b, b+a_n-1);
    cout << prev << " " << next;
}
```

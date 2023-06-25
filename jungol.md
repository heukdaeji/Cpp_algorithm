```cpp
#include <bits/stdc++.h>

using namespace std;

vector<int> wells[100001], bads[100001];
queue<int> q;
int N, M, X, a, b;

int main() {
    ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    cin >> N >> M >> X;
    for (int i = 0; i < M; i++) {
        cin >> a >> b;
        wells[a].push_back(b);
        bads[b].push_back(a);
    }
    q.push(X);
    int downs = -1;
    while (!q.empty()) {
        downs++;
    }
}```
+ 1561
+ 1637
+ 17616
+ 2842

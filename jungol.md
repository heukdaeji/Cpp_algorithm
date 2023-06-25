```cpp
#include <bits/stdc++.h>

using namespace std;

typedef struct person {
    int n, t;
} P;
int N, M, a;
vector<int> know[200001];
int knowtime[200001];
queue<P> q;

int main() {
    // ios::sync_with_stdio(0); cin.tie(0); cout.tie(0);
    cin >> N;
    for (int i = 1; i <= N; i++) {
        knowtime[i] = -1;
        while (true) {
            cin >> a;
            if (!a) break;
            know[i].push_back(a);
        }
    }
    cin >> M;
    for (int i = 0; i < M; i++) {
        cin >> a;
        knowtime[a] = 0;
        q.push({a, 0});
    }
    while (!q.empty()) {
        P x = q.front();
        q.pop();
        cout << x.n << " " << x.t << "\n";
        for (int i = 0; i < know[x.n].size(); i++) {
            if (knowtime[know[x.n][i]] != -1) continue;
            int cnt = 0;
            for (int j = 0; j < know[know[x.n][i]].size(); i++) {
                if (knowtime[know[know[x.n][i]][j]] != -1 && knowtime[know[know[x.n][i]][j]] != x.t+1) cnt++;
            }
            if (cnt*2 >= know[know[x.n][i]].size()) {
                knowtime[x.n] = x.t+1;
                q.push({know[x.n][i], x.t+1});
            }
        }
    }
    for (int i = 1; i <= N; i++) {
        cout << knowtime[i] << " ";
    }
}```
+ 1561
+ 1637
+ 19538
+ 17616
+ 2842

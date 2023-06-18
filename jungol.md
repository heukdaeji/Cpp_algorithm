```cpp
#include <iostream>
#include <algorithm>

using namespace std;

typedef struct date {
    int s, e;
} D;

bool cmp(D a, D b) {
    if (a.e == b.e) return a.s < b.s;
    return a.e > b.e;
}
bool ok;
int N, m, d1, d2;
D dates[100001];

int main() {
    ios::sync_with_stdio(false); cin.tie(0); cout.tie(0); 
    cin >> N;
    for (int i = 0; i < N; i++) {
        cin >> m >> dates[i].s;
        dates[i].s += 100 * m;
        cin >> m >> dates[i].e;
        dates[i].e += 100 * m;
        dates[i].s = max(301, dates[i].s);
        dates[i].e = min(1131, dates[i].e);
        ok = (dates[i].s == 301 || dates[i].e == 1130) || ok;
    }
    if (!ok) {
        cout << 0;
        return 0;
    }
    sort(dates, dates+N, cmp);
    for (int i = 0; i < N; i++) {
        cout << dates[i].s << " ~ " << dates[i].e << "\n";
    }
    int i = 0, ans = 1;
    while (dates[i].s != 301) i++;
    cout << dates[i].s << " " << dates[i].e << "\n";
    int e = dates[i].e;
    while (e != 1131) {
        i = 0;
        while (dates[i].s > e) {
            i++;
            if (i == N) {
                cout << 0;
                return 0;
            }
        }
        cout << dates[i].s << " " << dates[i].e << "\n";
        e = dates[i].e;
        ans++;
    }
    cout << ans;
}```
+ 2873

```cpp
#include <bits/stdc++.h>

using namespace std;

int X, Y, P, W; // 행, 열, 색종이, 잘못 칸
int xl, yl, maxx;
vector<pair<int, int>> a;

bool cmp(pair<int, int> x, pair<int, int> y) {
    if (x.second == y.second) return x.first < y.first;
    return x.second < y.second;
}

bool check(int x) {
    if (maxx > x) return false;
    int i = -1, amn = 0;
    while (i != W) {
        i++;
        int j = a[i].second;
        while ((j+x)>a[i].second && i < W) i++;
        cout << i << " ";
        amn++;
    }
    cout << x << ": " << amn << "\n";
    return P >= amn;
}

int main() {
    cin >> X >> Y >> P >> W;
    for (int i = 0; i < W; i++) {
        cin >> xl >> yl;
        maxx = max(maxx, xl);
        a.push_back({xl, yl});
    }
    sort(a.begin(), a.end(), cmp);
    // for (int i = 0; i < a.size(); i++) {
    //     cout << a[i].first << " " << a[i].second << "\n";
    // }
    int start = 1, end = min(X, Y);
    while (start < end) {
        int mid = (start+end)/2;
        if (check(mid)) end = mid;
        else start = mid+1;
    }
    cout << end;
}```
+ 2539
+ 1561
+ 1637

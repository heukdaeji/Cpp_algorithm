# 트리

* 코드:
```cpp
#include <iostream>
#include <vector>

using namespace std;

vector<int> trees[51];
int N, ans = 0, nodes, rem;

void dfs(int x) {
    if (x == rem) return;
    for (int i = 0; i < trees[x].size(); i++) {
        dfs(trees[x][i]);
    }
    if (trees[x].size() == 0 || (trees[x].size() == 1 && trees[x][0] == rem)) {
        ans++;
    }
}

int main() {
    int root;
    cin >> N;
    for (int i = 0; i < N; i++) {
        cin >> nodes;
        if (nodes == -1) {
          root = i;
          continue;
        }
        trees[nodes].push_back(i);
    }
    cin >> rem;
    trees[rem].clear();
    dfs(root);
    cout << ans;
}
```

# 트리의 지름

코드:
```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

vector<pair<int, int>> trees[100001];
int N;
int dists[100001] = {0, };
bool visiten[100001];

void dfs(int x) {
  visiten[x] = true;
  for (int i = 0; i < trees[x].size(); i++) {
    if (!visiten[trees[x][i].first]) {
      dists[trees[x][i].first] = dists[x] + trees[x][i].second;
      dfs(trees[x][i].first);
    }
  }
}

int main() {
  cin >> N;
  int from, to, dist;
  for (int i = 0; i < N; i++) {
    cin >> from;
    while (true) {
      cin >> to;
      if (to == -1)
        break;
      cin >> dist;
      trees[from].push_back({to, dist});
    }
  }
  dfs(1);
  int ans;
  for (int i = 1; i <= N; i++) {
    ans = max(ans, dists[i]);
  }
  cout << ans;
}
```

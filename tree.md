# 트리의 지름

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
}```

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

# 순열 사이클 (백준 10451번)

* 소스코드:
```cpp
#include <iostream>

using namespace std;

int T;
bool visiten[1001];
int arr[1001];

void dfs(int x)  {
    visiten[x] = true;
    if (!visiten[arr[x]]) dfs(arr[x]);
    return;
}

int main() {
    cin >> T;
    while (T--) {
        int ans = 0, N;
        cin >> N;
        for (int i = 1; i <= N; i++) {
            cin >> arr[i];
        }
        for (int i = 1; i <= N; i++) {
            if (!visiten[i]) {
                dfs(i);
                ans++;
            }
        }
        cout << ans << "\n";
        for (int i = 1; i <= N; i++) {
            visiten[i] = false;
        }
    }
}
```

# 토마토 (백준 7569번)
* 코드:
```cpp
#include <iostream>
#include <string.h>
#include <vector>

using namespace std;

int N, M, H;
typedef struct loc {
    int x, y, z;
} L;
int box[101][101][101];
bool visiten[101][101][101];
int dx[6] = {1, -1, 0, 0, 0, 0};
int dy[6] = {0, 0, 1, -1, 0, 0};
int dz[6] = {0, 0, 0, 0, 1, -1};
vector<L> tempbox;


void dfs(int x, int y, int z) {
    visiten[x][y][z] = true;
    for (int l = 0; l < 6; l++) {
        int cx = x + dx[l], cy = y + dy[l], cz = z + dz[l];
        if (0 > cx || cx >= H || 0 > cy || cy >= N || 0 > cz || cz >= M) continue;
        if (box[cx][cy][cz] == 0 && visiten[cx][cy][cz] == false) {
            tempbox.insert(0, {cx, cy, cz});
        }
    }
}

int main() {
    cin >> M >> N >> H;
    for (int i = 0; i < H; i++) {
        for (int j = 0; j < N; j++) {
            for (int k = 0; k < M; k++) {
                cin >> box[i][j][k];
            }
        }
    }
    int T = 0;
    while (true) {
        bool dfsed = false;
        for (int i = 0; i < tempbox.size(); i++) {
            dfs(tempbox[i].x, tempbox[i].y, tempbox[i].z);
            box[tempbox[i].x][tempbox[i].y][tempbox[i].z] = 1;
            tempbox.pop_back();
            dfsed = true;
        }
        if (!dfsed) {
            for (int i = 0; i < H; i++) {
                for (int j = 0; j < N; j++) {
                    for (int k = 0; k < M; k++) {
                        if (box[i][j][k] == 0) {
                            cout << -1;
                            return 0;
                        }
                    }
                }
            }
            cout << T-1;
            return 0;
        }
        T++;
    }
}
```

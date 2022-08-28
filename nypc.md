# 1번. 사진작가

* 투 포인터를 이용하면 쉽게 해결할 수 있다.
*```cpp
#include <iostream>

using namespace std;

int st[200001];
int nums[1000001] = {0, };
int N;

int main() {
	cin.tie(0); cout.tie(0); ios_base::sync_with_stdio(0);
	cin >> N;
	for (int i = 0; i < N; i++) {
		cin >> st[i];
	}
	int s = 0, e = 0;
	int ans = 0;
	bool joongbok = false;
	while (e < N) {
		nums[st[e]]++;
		if (nums[st[e]] == 2) {
			joongbok = true;
		} else {
			ans = max(e-s+1, ans);
		}
		if (joongbok) {
			while (st[s] != st[e]) {
				nums[st[s]]--;
				s++;
			}
			s++;
			nums[st[e]]--;
			joongbok = false;
		}
		e++;
	}
	cout << ans;
}```

# 4번. 물고기 양식장

```cpp
#include <iostream>
#include <string>
#include <cmath>
#include <algorithm>
#include <vector>

using namespace std;

typedef struct fish {
	int exist, num, r1, r2, c1, c2;
} F;

vector<F> fishes;

int eggs[100001] = {0, };
int n, k, R1, R2, C1, C2;
int N, M, K, Q;

int main() {
	cin >> N >> M >> K >> Q;
	for (int i = 0; i < Q; i++) {
		cin >> n >> k >> R1 >> C1 >> R2 >> C2;
		if (n == 1)
			fishes.push_back({n, k, R1, R2, C1, C2});
		else if (n == 2) {
			for (int j= 0; j < fishes.size(); j++) {
				if (fishes[j].num == k) {
					fishes[j].exist = 0;
					break;
				}
			}
		}
		int ans = 0;
		for (int j = 0; j < fishes.size(); j++) {
			if (!fishes[j].exist) continue;
			for (int l = j+1; l < fishes.size(); l++) {
				if (!fishes[l].exist) continue;
				if (max(fishes[l].r1, fishes[j].r1) <= min(fishes[l].r2, fishes[j].r2)) {
					if (max(fishes[l].c1, fishes[j].c1) <= min(fishes[l].c2, fishes[j].c2)) {
						eggs[j] += (min(fishes[l].c2, fishes[j].c2)-max(fishes[l].c1, fishes[j].c1)+1)*(min(fishes[l].r2, fishes[j].r2)-max(fishes[l].r1, fishes[j].r1)+1);
						eggs[l] += (min(fishes[l].c2, fishes[j].c2)-max(fishes[l].c1, fishes[j].c1)+1)*(min(fishes[l].r2, fishes[j].r2)-max(fishes[l].r1, fishes[j].r1)+1);
					}
				}
			}
		}
	}
	for (int i = 0; i < K; i++) {
		cout << eggs[i] << "\n";
	}
}```

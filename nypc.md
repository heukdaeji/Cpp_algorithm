# 1번. 사진작가

* 투 포인터를 이용하면 쉽게 해결할 수 있다.
```cpp
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

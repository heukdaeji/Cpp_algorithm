```cpp
#include <iostream>
#include <algorithm>

using namespace std;

int heap[100001], hn;

void push(int x) {
  heap[++hn] = x;
  for (int i = hn; i > 1; i /= 2) {
    if (heap[i/2] > heap[i]) swap(heap[i/2], heap[i]);
    else break;
  }
}

int pop() {
    int ans = heap[1];
    heap[1] = heap[hn];
    heap[hn--] = 0;
    for (int i = 1; i*2 <= hn;) {
        if (heap[i] < heap[i*2] && heap[i] < heap[i*2+1]) break;
        else if (heap[i*2] > heap[i*2+1]) {
            swap(heap[i], heap[i*2]);
            i = 2*i;
        } else {
            swap(heap[i], heap[2*i+1]);
            i = 2*i+1;
        }
    }
    return ans;
}

int main() {
  int t;
  cin >> t;
  for (int i = 0; i < t; i++) {
    int x;
    cin >> x;
    push(x);
  }
  
  for (int i = 1; i <= t; i++) {
    for (int j = 1; j <= t; j++) {
      cout << heap[j] << " ";
    }
    cout << "\n" << pop() << "\n";
  }
}
```

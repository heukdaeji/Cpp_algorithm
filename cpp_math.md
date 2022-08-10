# 1. 소인수분해
* n을 소인수분해 했을 떄, 나타날 수 있는 소인수중에서 2번째로 큰 값은 $\sqrt{}$ n 이다.
* 이 숫자 미만 까지 전부 나눌 수 있는 지 체크한다.
* 마지막은 안 나눠진 소수가 있는지 체크한다.

* 전체 코드:
```cpp
#include <iostream>

using namespace std;

int n;

int main() {
   cin >> n;
   for (int i = 2; i * i < n; i++) {
      while (n % i == 0) {
          n /= i;
          cout << i << "\n";
      }
   }
   if (n != 1) cout << n << "\n";
   return 0;
}
```

# 2. 팩토리얼
* 1 ~ n까지 곱을 나타냄. ex) $n!=n \times (n-1) \times (n-2) \times \cdots \times 3 \times 2 \times 1 $
* 반복문 or 재귀함수
* dp로 표현하면 $f_n = n \times f_{n-1}$

* 전체 코드:
```cpp
#include <iostream>

using namespace std;

int factorialnum(int n) {
    if (n == 0) return 1;
    return n * factorialnum(n-1);
}
int N;

int main() {
   cin >> N;
   cout << factorialnum(N) << "\n";
}
```

# 3. 최대공약수
* [백준 2609번](https://www.acmicpc.net/problem/2609) (with 최소공배수)
* 유클리드 호제법을 이용한다.

* 전체 코드:
```cpp
#include <iostream>

using namespace std;

int gcd(int a, int b) {
    if (a == 0) return b;
    else if (b == 0) return a;
    else {
        if (a > b) {
            return gcd(b, a % b);
        }
        else {
            return gcd(a, b % a);
        }
    }
}

int main() {
   int n, m;
   cin >> m >> n;
   cout << gcd(m, n) << "\n";
}
```

# 4. 최소공배수
* 간단히 반복문을 사용한다.
* a * n이 b로 나누어 떨어지면 a * n이 최소공배수이다.

* 전체 코드:
```cpp
#include <iostream>

using namespace std;

int lcm(int a, int b) {
    int n = 1;
    while (1) {
        if (n * a % b == 0) {
            return n*a;
        }
        n++;
    }
}

int main() {
   int m, n;
   cin >> m >> n;
   cout << lcm(m, n) << "\n";
}
```

# 5. 진법
## 10진법 -> n진법 [백준 11005번](https://www.acmicpc.net/problem/11005)
* 10으로 쭉 나누고 결과를 뒤집으면 된다.

* 전체 코드:
```cpp
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main() {
   int n, b;
   cin >> n >> b;
   string ans = "";
   while (n > 0) {
       int r = n % b;
       if (r < 10) {
           ans += (char)(r + '0');
       } else {
           ans += (char)(r - 10 + 'A');
       }
       n /= b;
   }
   reverse(ans.begin(), ans.end());
   cout << ans;
   return 0;
}
```

## n진법 -> 10진법 [백준 2745번](https://www.acmicpc.net/problem/2745)
* 진법의 0 ~ 자릿수-1 까지의 b의 제곱을 이용하여 계산된 결과를 더함.
* 0~9진법수가 들어오면, 지금까지 구한 값(ans)에 b를 곱하고, 현재 자릿수의 값을 더함.
* 11진법 이상이라면, 10을 더하고 'A'와의 차잇값을 더한다. (ans * b + (s[i] - 'A' + 10)

* 전체 코드:
```cpp
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main() {
   int ans = 0, b;
   string s;
   cin >> s;
   cin >> b;
   for (int i = 0; i < s.size(); i++) {
       if ('0' <= s[i] && s[i] <= '9') {
           ans = ans * b + (s[i] - '0');
       } else {
           ans = ans * b + (s[i] - 'A' + 10);
       }
   }
   cout << ans << "\n";
   return 0;
}
```
## 2진수 -> 8진수 [백준 1373번](https://www.acmicpc.net/problem/1373)

## 소수

## 골드바흐의 추측

### 소스 코드
```cpp
#include <iostream>
#include <string>
#include <cmath>
#include <algorithm>
#define BIGNUM 10001

using namespace std;

int x;
int prime[5001], pn;
bool num[BIGNUM] = {false, };

int nearIndex(int a) {
    int idx, tmp, min = 10001;
    for (int i = 0; i < pn; i++) {
        tmp = prime[i] - a;
        if (abs(min) > abs(tmp)) {
            min = tmp;
            idx = i;
        }
    }
    return idx;
}

int main() {
    num[1] = true;
    int N; cin >> N;
    for (int i = 2; i <= BIGNUM; i++) {
        if (num[i] == false) {
            prime[pn++] = i;
            for (int j = i * i; j <= BIGNUM; j += i) {
                num[j] = true; 
            }
        }
    }
    for (int i = 0; i < N; i++) {
        cin >> x;
        for (int j = nearIndex(x/2); j >= 0; j--) {
            if (num[x-prime[j]] == false) {
                cout << prime[j] << " " << x-prime[j] << "\n";
                break;
            }
        }
    }
}
```

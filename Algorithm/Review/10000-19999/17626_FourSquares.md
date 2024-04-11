# BOJ 17626 Four Squares

## 사고 흐름

이 문제는 브루트포스와 DP 두 가지 방법으로 해결할 수 있다.

중복되는 연산을 제거해주기 위해서 DP로 접근하였다. 가장 먼저 인덱스에 해당하는 값을 만들 수 있는 최소 개수의 제곱수 합을 저장하는 DP 테이블을 선언 했다.

1부터 최대 N 까지 제곱수는 그 자체로 표현할 수 있기 때문에 DP 테이블에서 1로 초기화 해주었다.

그 다음 Top-Down 방식으로 `target`에 가장 가까운 제곱 수 부터 빼나가면서 값을 재귀적으로 탐색하고 이미 계산한 값이라면 해당 DP 값을 반환하도록 했다.

점화식은 다음과 같다.

dp[i] = Math.min(dp[i], dp[i - j * j] + 1);

## 복기

이 문제를 부르트포스로도 풀 수 있는데, 문제 자체에 힌트가 있다.

"모든 자연수는 넷 혹은 그 이하의 제곱수의 합으로 표현할 수 있다고 증명" 에서 알 수 있듯이 정답이 될 수 있는 값은 1 부터 4 까지이다.

```java
public static int solve() {
    for (int i = 1; i * i <= N; i++) {
        if (i * i == N) {
            return 1;
        }
    }
    for (int i = 1; i * i <= N; i++) {
        double sqrtA = Math.sqrt(N - i * i);
        if (sqrtA == Math.floor(sqrtA)) {
            return 2;
        }
    }
    for (int i = 1; i * i <= N; i++) {
        for (int j = 1; j * j <= N - i * i; j++) {
            double sqrtA = Math.sqrt(N - i * i - j * j);
            if (sqrtA == Math.floor(sqrtA)) {
                return 3;
            }
        }
    }
    return 4;
}
```
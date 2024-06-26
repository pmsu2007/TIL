# BOJ 13144 List of Unique Numbers

## 사고 흐름

주어진 입력의 크기가 100,000으로 크다. 따라서, O(N) ~ O(NlogN) 시간 내에 해결해야 겠다고 생각했다. 

또한, 연속한 무언가를 구해야하는 문제이므로 투 포인터를 가장 먼저 생각하였다.

가장 쉬운 방법인 O(N^2)이 걸리는 연산으로 해결할 수 있지만 방문 정보를 통해 불필요한 연산을 제거할 수 있다.

1. 오른쪽 포인터를 하나씩 늘려가면서 각 값에 대해서 방문하지 않았다면, 방문처리를 한다.
2. 만약, 이미 방문했던 값이라면 해당 값 이전의 수열에 대해서 경우의 수를 계산(`r - l`)한다.
   1. 왼쪽 포인터에 해당하는 값의 방문 처리를 해제하고 한칸 앞으로 이동한다.
3. 위 과정을 전체 배열에 대해 수행한다.

## 복기

하나도 중복되는 값이 없을 경우에 결과 값 최대가 된다. 즉, 결과 값이 최대 100,000 * 100,001 / 2 = 약 50억 이므로 `int`형의 범위를 벗어남으로 자료형에 주의하자.. 

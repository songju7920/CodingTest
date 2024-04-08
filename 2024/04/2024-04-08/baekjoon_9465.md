## 백준 9465번 스티커

### 문제 해결과정

- 문제 분류 : DP
- 문제 목표 : 뗄 수 있는 스티커의 점수의 최댓값을 구하는 프로그램을 작성하라
- 풀이과정
  1. DP를 Idx 1 까지 초기화한다.
     (idx 0은 스티커 가치 입력값 그대로, idx 2는 스티커 가치 입력값 + DP[0][자신의 idx와 반대되는 idx])
  2. idx 3부터는 최대값이 나오는 패턴을 따라 다음 점화식을 따르면 된다.
     max(DP[i - 1][자신의 idx가 0이면 1, 1이면 0], DP[i - 2][0], DP[i - 2][1]) + stickers[i][자신의 idx]
  3. max(DP[N - 1])를 출력한다.

### 풀이 코드

```python
T = int(input())

for _ in range(T):
  N = int(input())
  stickers = [list(map(int, input().split())) for _ in range(2)]

  if N == 1:
    print(max(stickers[0][0], stickers[1][0]))
    continue

  DP = [[0] * 2 for _ in range(N)]
  DP[0] = [stickers[0][0], stickers[1][0]]
  DP[1] = [stickers[0][1] + DP[0][1], stickers[1][1] + DP[0][0]]

  for i in range(2, N):
    DP[i][0] = max(DP[i - 1][1], DP[i - 2][1], DP[i - 2][0]) + stickers[0][i]
    DP[i][1] = max(DP[i - 1][0], DP[i - 2][1], DP[i - 2][0]) + stickers[1][i]

  print(max(DP[N - 1]))
```

한줄 회고 : 그냥 모든 DP 문제가 그렇듯, 점화식만 떠올려내면 쉬운 문제였다.

### 다른사람의 풀이

```python
t = int(input())
max_value = []
for i in range(0, t):
    n = int(input())
    a = list(map(int, input().split()))
    b = list(map(int, input().split()))

    if n < 2:
        max_value.append(max(a[0], b[0]))
        continue

    dp_a = [a[0], b[0] + a[1]]
    dp_b = [b[0], a[0] + b[1]]

    for j in range(2, n):
        dp_a.append(a[j] + max(dp_b[j-1], dp_b[j-2]))
        dp_b.append(b[j] + max(dp_a[j-1], dp_a[j-2]))

    max_value.append(max(dp_a[-1], dp_b[-1]))

for i in range(0, t):
    print(max_value[i])
```

이 풀이는 나와 동일한 DP를 사용한 풀이지만, 특이한점이 몇개 있다.
특히한게, DP를 위아래를 분리하여 사용한게 참 특이했다.
내가 직접 실험해보니, 이렇게 분리하여 입력 & DP에 저장하는 방법이 시간복잡도가 눈에 띄게 줄어들었다.

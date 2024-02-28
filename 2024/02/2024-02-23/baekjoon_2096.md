## 프로그래머스 2096번 **내려가기**

### 문제 해결과정

- 문제 분류 : DP
- 문제 특이사항: 매우 적은 메모리 제한(4MB)
- 반환해야 하는 값 : 내려올때의 점수를 [가장 최대값, 가장 적은값] 형식으로 출력하라
- 풀이과정
  1. 처음 층부터 탐색을 시작한다
  2. 위에서 접근할 수 있는 최소값, 최대값을 DP에 기록
  3. 값 출력하기

### 풀이 코드

```python
import sys
input = sys.stdin.readline

N = int(input())

Board = list(map(int, input().split()))
DP = [[num, num] for num in Board]
movement = [-1, 0, 1]

for i in range(1, N):
  result = []
  Board = list(map(int, input().split()))

  for j in range(0, 3):
    minNum, maxNum = 0, 1e9
    for move in movement:
      nx = j + move

      if 0 <= nx < 3:
        if minNum < DP[nx][0] + Board[j]:
          minNum = DP[nx][0] + Board[j]
        if maxNum > DP[nx][1] + Board[j]:
          maxNum = DP[nx][1] + Board[j]

    result.append([minNum, maxNum])
  DP = result

print(max(DP, key=lambda x: x[0])[0], min(DP, key=lambda x: x[1])[1])
```

코드 시간복잡도 (빅오) : O(n^2)

한줄 회고 : 이 문제의 가장 어려웠던 점은 메모리가 정말 적었다는 점이다. 때문에, 2차원 배열을 사용하지 않고 배열들을 재사용하면서 해결했다.

### 다른사람의 풀이

```python
import sys
input = sys.stdin.readline

n  = int(input())

dpMax = [0]*3
dpMin = [10e10]*3

for i in range(n):
    cur = list(map(int,input().split()))
    if i  == 0 :
        for i in range(3):
            dpMax[i] = cur[i]
            dpMin[i] = cur[i]

    else:
        nextMax = [0,0,0]
        nextMin = [0,0,0]
        nextMax[0] = max(dpMax[0], dpMax[1]) + cur[0]
        nextMax[2] = max(dpMax[2], dpMax[1]) + cur[2]
        nextMax[1] = max(dpMax[0], dpMax[1], dpMax[2]) + cur[1]

        nextMin[0] = min(dpMin[0], dpMin[1]) + cur[0]
        nextMin[2] = min(dpMin[2], dpMin[1]) + cur[2]
        nextMin[1] = min(dpMin[0], dpMin[1], dpMin[2]) + cur[1]

        dpMax = nextMax
        dpMin = nextMin

print(max(dpMax) , min(dpMin))
```

이 풀이는 메모리 사용량은 비슷하지만 (1차원 배열 3개 사용) 시간복잡도가 200ms정도 빠르다
아무래도 가장 큰 이유는 2중 반복문의 사용때문인것 같다.

실제로 밑에처럼 코드를 재설계했더니 속도가 560ms에서 364ms로 약 200ms정도가 빨라졌다.

```python
import sys
input = sys.stdin.readline

N = int(input())

Board = list(map(int, input().split()))
DP = [[num, num] for num in Board]
movement = [-1, 0, 1]

for i in range(1, N):
  result = []
  Board = list(map(int, input().split()))

  result = [[0, 0], [0, 0], [0, 0]]
  result[0][0] = max(DP[0][0], DP[1][0]) + Board[0]
  result[2][0] = max(DP[2][0], DP[1][0]) + Board[2]
  result[1][0] = max(DP[0][0], DP[1][0], DP[2][0]) + Board[1]

  result[0][1] = min(DP[0][1], DP[1][1]) + Board[0]
  result[2][1] = min(DP[2][1], DP[1][1]) + Board[2]
  result[1][1] = min(DP[0][1], DP[1][1], DP[2][1]) + Board[1]

  DP = result

print(max(DP, key=lambda x: x[0])[0], min(DP, key=lambda x: x[1])[1])
```

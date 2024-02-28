## 프로그래머스 16234번 인구 이동

### 문제 해결과정

- 문제 분류 : 시뮬레이션, BFS
- 반환해야 하는 값 : 인구이동을 하는 횟수를 구하라
- 풀이과정
  1. 각 칸의 연합구성을 체크한다
  2. 연합의 총합을 연합국가의 개수로 나눠서 계산한다.
  3. 만약 전의 그래프와 변화가 없으면 반복을 종료한다

### 풀이 코드

```python
import sys
from collections import deque
from copy import deepcopy
input = sys.stdin.readline

N, L, R = map(int, input().split())

graph = [[] for _ in range(N)]
movement = [[1, 0], [-1, 0], [0, 1], [0, -1]]

for i in range(N):
  graph[i] = list(map(int, input().split()))

def BFS(start, visited):
  unity = [start]
  unitySum = graph[start[0]][start[1]]
  queue = deque([start])
  visited[start[0]][start[1]] = True

  while queue:
    cx, cy = queue.popleft()

    for move in movement:
      nx, ny = cx + move[0], cy + move[1]
      if 0 <= nx < N and 0 <= ny < N and not visited[nx][ny] and L <= abs(graph[cx][cy] - graph[nx][ny]) <= R:
        unitySum += graph[nx][ny]
        visited[nx][ny] = True
        unity.append([nx, ny])
        queue.append([nx, ny])

  unityVal = unitySum // len(unity)
  for x, y in unity:
    graph[x][y] = unityVal

answer = 0
while True:
  beforeGraph = deepcopy(graph)
  visited = [[False] * N for _ in range(N)]

  for i in range(N):
    for j in range(N):
      if not visited[i][j]:
        BFS([i, j], visited)

  if beforeGraph == graph:
    break

  answer += 1

print(answer)
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 이런 형식의 문제는 처음 풀어보는데 생각보다 쉬웠다.

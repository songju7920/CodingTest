## 백준 10026번 적록색약

### 문제 해결과정

- 문제 분류 : 그래프 이론, DFS, BFS
- 반환해야 하는 값 : 그래프가 주어졌을때 일반인이 보는 구역의 개수와 적록색약인 사람이 보는 구역의 개수를 구하라
- 풀이과정
    1. 그래프를 입력받는다
    2. 일반인이 보는 구역별로 탐색해 개수를 계산한다
    3. 적록색약인 사람이 보는 구역별로 탐색해 개수를 계산한다

### 풀이 코드

```python
from collections import deque

N = int(input())
graph = [input() for _ in range(N)]
movement = [[1, 0], [-1, 0], [0, 1], [0, -1]]

visited1 = [[False for _ in range(N)] for _ in range(N)]
visited2 = [[False for _ in range(N)] for _ in range(N)]

def BFS1(start, target):
  queue = deque([start])
  visited1[start[0]][start[1]] = True

  while queue:
    point = queue.popleft()
    for move in movement:
      nx, ny = move[0] + point[0], move[1] + point[1]
      if 0 <= nx < N and 0 <= ny < N and not visited1[nx][ny] and graph[nx][ny] == target:
        visited1[nx][ny] = True
        queue.append([nx, ny])
  
def BFS2(start, target):
  queue = deque([start])
  visited2[start[0]][start[1]] = True

  while queue:
    point = queue.popleft()
    for move in movement:
      nx, ny = move[0] + point[0], move[1] + point[1]
      if 0 <= nx < N and 0 <= ny < N and not visited2[nx][ny]:
        if target == 'R' and graph[nx][ny] == 'G' or target =='G' and graph[nx][ny] == 'R' or target == graph[nx][ny]:
          visited2[nx][ny] = True
          queue.append([nx, ny])

result = [0, 0]
for i in range(N):
  for j in range(N):
    if not visited1[i][j]:
      result[0] += 1
      BFS1([i, j], graph[i][j])
    if not visited2[i][j]:
      result[1] += 1
      BFS2([i, j], graph[i][j])
      

print(*result)
```

코드 시간복잡도 (빅오) : 약 O(n^2)

한줄 회고 : 코드가 조금 더러워서 마음에 안들었던 풀이였다..

### 다른사람의 풀이

```jsx
import sys
sys.setrecursionlimit(10000000)

N = int(input())
graph = []

for _ in range(N):
  graph.append(list(input()))

visited = [[0]*N for _ in range(N)]

dx = [1,-1,0,0]
dy = [0,0,1,-1]
cnt_1 = 0
cnt_2 = 0

def DFS(x,y):
  visited[x][y] = 1
  current = graph[x][y]
  for i in range(4):
    nx = x+dx[i]
    ny = y+dy[i]
    if 0<=nx<N and 0<=ny<N and graph[nx][ny] == current:
      if visited[nx][ny] == 0:
        DFS(nx,ny)
    

for i in range(N):
  for j in range(N):
    if visited[i][j] == 0:
      DFS(i,j)
      cnt_1 += 1

for i in range(N):
  for j in range(N):
    if graph[i][j] == 'G':
      graph[i][j] = 'R'

visited = [[0]*N for _ in range(N)]

for i in range(N):
  for j in range(N):
    if visited[i][j] == 0:
      DFS(i,j)
      cnt_2 += 1

print(cnt_1, cnt_2)
```

이 풀이가 마음에 들었던점은 나처럼 복잡한 IF문을 사용하지 않아 훨씬 코드가 깔끔했담,

그리고 나와 이 사람의 풀이중 가장 큰 차이점은 이사람은 DFS, 난 BFS를 사용했다는 점이다.
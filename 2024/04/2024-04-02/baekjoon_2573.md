## 백준 2573번 빙산

### 문제 해결과정

- 문제 분류 : DFS/BFS
- 반환해야 하는 값 : 빙산이 2개로 갈라지는 때는 몇년 후인지, 만약 다 녹을때까지 나눠지지 않는다면 0을 출력
- 풀이과정
    1. N, M과 그래프를 입력받는다.
    2. 한줄한줄 돌아다면서, 0이 아닌 숫자를 발견하면 거기서부터 탐색을 시작란다
    3. 탐색시 인접해있는 바다 수 만큼 해당 그래프에서 숫자 빼기
    4. 나누어졌다면 반복 탈출, 아직 1개면 계속 진행, 0개 남았다면 1을 출력한다

### 풀이 코드

```python
from collections import deque

answer = 0
N, M = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(N)]
movement = [[1, 0], [-1, 0], [0, 1], [0, -1]]

def BFS(start, visit):
    queue = deque([start])
    visit[start[0]][start[1]] = True
    
    while queue:
        x, y = queue.popleft()
        
        for mx, my in movement:
            nx, ny = x + mx, y + my
            
            if 0 <= nx < N and 0 <= ny < M and not visit[nx][ny]:
                if graph[nx][ny] != 0:
                    visit[nx][ny] = True
                    queue.append([nx, ny])
                elif graph[x][y] > 0:
                    graph[x][y] -= 1

while True:
    part = 0
    visit = [[False] * M for _ in range(N)]
    
    for i in range(N):
        for j in range(M):
            if graph[i][j] != 0 and not visit[i][j]:
                BFS([i, j], visit)
                part += 1

    if part > 1: break
    if part == 0:
        answer = 0
        break
    answer += 1
    
print(answer)
```

한줄 회고 : 이 문제는 빙산이 녹는것을 처리하는게 힘들었던 문제이다.

### 다른사람의 풀이

```python
import sys
from collections import deque
input = sys.stdin.readline

direction  = [(0, 1), (0, -1), (1, 0), (-1, 0)]

def bfs(x, y):
    queue = deque([(x, y)])
    visited[x][y] = True
    sea_list = []
    
    while queue:
        x, y = queue.pop()
        sea = 0
        for dx, dy in direction:
            nx = x + dx
            ny = y + dy
            
            if 0 <= nx < n and 0 <= ny < m:
                if not graph[nx][ny]:
                    sea += 1
                elif graph[nx][ny] and not visited[nx][ny]:
                    queue.append((nx, ny))
                    visited[nx][ny] = True
        if sea > 0:
            sea_list.append((x, y, sea))
    
    for x, y, sea in sea_list:
        graph[x][y] = max(0, graph[x][y] - sea)
    
    return 1

n, m = map(int, input().split())
graph = [list(map(int, input().split())) for _ in range(n)]

ice = []

for i in range(n):
    for j in range(m):
        if graph[i][j]:
            ice.append((i, j))

year = 0

while ice:
    visited = [[False] * m for _ in range(n)]
    del_list = []
    group = 0
    
    for i, j in ice:
        if graph[i][j] and not visited[i][j]:
            group += bfs(i, j)
        if graph[i][j] == 0:
            del_list.append((i, j))
    
    if group > 1:
        print(year)
        break
    
    ice = list(set(ice) - set(del_list))
    year += 1

if group < 2:
    print(0)

```

코드 길이는 길다. 허나, 내 코드의 실행시간은 3196ms인데 이 코드의 실행시간은 1900ms이다. 이유는 아마도 바로바로 뻬지 않고, 한꺼번에 모아서 빙산의 녹은정도를 처리했기 때문인것 같다
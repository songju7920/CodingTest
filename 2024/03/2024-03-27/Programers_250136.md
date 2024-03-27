# [PCCP 기출문제] 2번 / 석유 시추

## 프로그래머스 250136번 석유 시추

### 문제 해결과정

- 문제 분류 : BFS/DFS, 구현
- 반환해야 하는 값 : 석유 시추시 가장 많이 얻을 수 있는 석유의 양
- 풀이과정
  1. 맵의 가로길이 만큼 answer 배열을 생성한다.
  2. 맵을 위에서부터 한줄씩 왼쪽에서 오른쪽으로 탐색을 시작한다.
  3. 만약 1(석유 존재)이고 이 1과 연결된 다른 1을 방문한적이 없어 Visit 배열이 False라면 다음 동작을 수행한다.
     1. BFS를 실행하여 인접해있는 1의 개수와 맵의 어느 열에서 접근할 수 있는지를 조사한다
     2. 접근할 수 있는 행의 Answer을 1의 총 개수만큼 올린다
  4. answer배열의 최대값을 조회한다.

### 풀이 코드

```python
from collections import deque

def BFS(start, graph, visit):
    queue = deque([start])
    visit[start[0]][start[1]] = True
    movement = [[1, 0], [-1, 0], [0, 1], [0, -1]]

    result = 1
    visitedRows = []

    while queue:
        x, y = queue.popleft()
        visitedRows.append(y)

        for mx, my in movement:
            nx, ny = x + mx, y + my

            if 0 <= nx < len(graph) and 0 <= ny < len(graph[0]) and graph[nx][ny] and not visit[nx][ny]:
                result += 1
                visit[nx][ny] = True
                queue.append([nx, ny])

    return list(set(visitedRows)), result

def solution(land):
    answer = [0] * len(land[0])
    visit = [[False] * len(land[0]) for _ in range(len(land))]

    for i in range(len(land)):
        for j in range(len(land[0])):
            if not visit[i][j] and land[i][j]:
                visitedRows, result = BFS([i, j], land, visit)

                for row in visitedRows:
                    answer[row] += result


    return max(answer)
```

코드 시간복잡도 (빅오) : O(n^2)

한줄 회고 : 이 문제는 시간복잡도때문에 고생했던 문제로, 이런 문제는 굉장히 오랜만이여서 새로웠다. 처음엔 시뮬레이션으로 풀면 통과 될줄 알았으나, 더 효율적인 방법을 생각해야 했던 문제였다.

### 다른사람의 풀이

```python
def solution(land):
    n, m = len(land), len(land[0])
    visited = [[True]*m for _ in range(n)]
    delta = [(1,0),(-1,0),(0,1),(0,-1)]
    oil_cnt = [0]*m
    for i in range(n):
        for j in range(m):
            if land[i][j] and visited[i][j]:
                visited[i][j] = False
                s = [(i,j)]
                col = set()
                oil = 0
                while s:
                    x, y = s.pop()
                    col.add(y)
                    oil += 1
                    for dx, dy in delta:
                        X, Y = x+dx, y+dy
                        if 0<=X<n and 0<=Y<m and land[X][Y] and visited[X][Y]:
                            visited[X][Y] = False
                            s.append((X,Y))
                for y in col:
                    oil_cnt[y] += oil
    return max(oil_cnt)
```

나와 풀이는 유사하나, 코드가 조금 더 간결한 경우이다. 다만 BFS쪽을 다른 함수로 분리했다면 더 좋았을것 같다.

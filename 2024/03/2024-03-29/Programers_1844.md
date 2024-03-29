# Programers_1844

## 프로그래머스 1844번 게임 맵 최단거리

### 문제 해결과정

- 문제 분류 : DFS/BFS
- 반환해야 하는 값 : 상대 팀 진영에 도착하기 위해서 지나가야 하는 칸의 개수의 최솟값을 반환 
                            단, 상대 팀 진영에 도착할 수 없을 때는 -1 반환
- 풀이과정
    1. Visit 배열을 False로 놓지 않고, -1로 놓고, 이동 횟수를 표시하도록 설정하여 답안으로 쓸 수 있도록 표시함
    2. 평범한 BFS 로직 구성
    3. Visit[N - 1][M - 1]이 답안이므로, 반환함

### 풀이 코드

```python
from collections import deque

def solution(maps):
    N, M = len(maps), len(maps[0])
    answer = 0
    movement = [[1, 0], [-1, 0], [0, 1], [0, -1]]
    visited = [[-1] * M for _ in range(N)]
    
    def BFS(start):
        queue = deque([start])
        visited[start[0]][start[1]] = 1
        
        while queue:
            x, y = queue.popleft()
            
            if x == N - 1 and y == M - 1: break
            
            for mx, my in movement:
                nx, ny = x + mx, y + my
                if 0 <= nx < N and 0 <= ny < M and visited[nx][ny] == -1 and maps[nx][ny]:
                    visited[nx][ny] = visited[x][y] + 1
                    queue.append([nx, ny])
    
    
    BFS([0, 0])
    return visited[N - 1][M - 1]
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 쉬운 DFS/BFS 문제였다
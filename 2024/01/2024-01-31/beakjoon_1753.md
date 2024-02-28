## 프로그래머스 1753번 최단경로

### 문제 해결과정

- 문제 분류 : 다익스트라 알고리즘
- 반환해야 하는 값 : 출발점에서 각 노드까지의 최단거리
- 풀이과정
  1. 그래프 입력 받기
  2. 우선순위 큐를 이용한 다익스트라 알고리즘으로 최단경로 탐색
  3. 각각 출력하기

### 풀이 코드

```jsx
import heapq
import sys

input = sys.stdin.readline

N, M = map(int, input().split())
start = int(input())

graph = [[] for _ in range(N + 1)]

for _ in range(M):
  startPoint, endPoint, dis = map(int, input().split())
  graph[startPoint].append([endPoint, dis])

def dijkstra():
  dist = [1e9] * (N + 1)
  dist[start] = 0
  queue = []
  heapq.heappush(queue, (0, start))

  while queue:
    cur_dis, cur_point = heapq.heappop(queue)

    if cur_dis > dist[cur_point]:
      continue

    for next, next_dis in graph[cur_point]:
      if dist[next] > cur_dis + next_dis:
        dist[next] = cur_dis + next_dis
        heapq.heappush(queue, (dist[next], next))

  return dist

result = dijkstra()
for i in range(1, N + 1):
  print(result[i] if result[i] != 1e9 else 'INF')
```

코드 시간복잡도 (빅오) : O(V2log(V))

한줄 회고 : 처음 다익스트라 알고리즘을 썼던 문제였는데 생각보다 신박한 방법이라 신기했다.

### 새로 알게된점

- 다익스트라 알고리즘
  최단거리를 찾는 알고리즘으로, 각 간선의 가중치를 고려한 알고리즘
  BFS와 논리는 비슷하나, 우선순위의 존재와 가중치의 존재가 차이점이다.

## 백준 1068번 트리

문제 해결과정

- 문제 분류 : BFS, 그래프 이론
- 반환해야 하는 값 : 특정 노드를 삭재했을때의 리프노드 개수
- 풀이과정
  1. 입력값을 바탕으로 graph와 시작노드(최상위 노드)파악
  2. BFS 탐색 시작
     1. 각 노드에 대하여:
     2. 만약 이번 노드가 리프노드면 result +=1 을 실행한후 다음 노드를 탐색
     3. 만약 이 노드가 리프노드가 아니라면, 이 노드에 연결된 노드들을 가지고 다음 동작 실행
        1. 만약 다음 노드를 방문한적이 없고, 삭제해야하는 노드가 아니라면 queue에 append.
        2. 만약 삭제해야 하는 노드고, 이 노드가 지워지면 부모노드가 리프노드가 되는경우 result += 1

### 풀이 코드

```jsx
from collections import deque

N = int(input())
data = list(map(int, input().split()))
target = int(input())

graph = [[] for _ in range(N)]
startNode = 0
for i in range(N):
  if data[i] != -1:
    graph[data[i]].append(i)
  else:
    startNode = i

def BFS(startNode):
  result = 0
  queue = deque([startNode])
  visited = [False] * N
  visited[startNode] = True
  if startNode == target:
    return 0

  while queue:
    curruntNode = queue.popleft()

    if len(graph[curruntNode]) == 0:
      result += 1
      continue

    for nextNode in graph[curruntNode]:
      if not visited[nextNode] and nextNode != target:
        queue.append(nextNode)
        visited[nextNode] = True
      elif nextNode == target and len(graph[curruntNode]) == 1:
        result += 1

  return result

print(BFS(startNode))
```

코드 시간복잡도 (빅오) : O(n^2)

한줄 회고 : 한 노드가 삭제되면 그 노드의 부모노드가 리프노드가 되는 경우를 제외하면, 정석적인 BFS문제였다.

### 다른사람의 풀이

```jsx
n = int(input())
edges = list(map(int,input().split()))
delete_node = int(input())

adj_list = [[]for _ in range(n)]
root_node = -1

for i in range(len(edges)):
    if i == delete_node and edges[i] == -1:
        print(0)
        exit(0)
    if i == delete_node or edges[i] == delete_node:
        continue
    if edges[i] == -1:
        root_node = i
        continue
    adj_list[edges[i]].append(i)

count = 0
def dfs(node):
    global count
    if not adj_list[node]:
        count += 1
        return

    for adj_node in adj_list[node]:
        dfs(adj_node)

    return

dfs(root_node)

print(count)
```

이사람은 나와 다르게 DFS를 이용하여 이 문제를 풀었다. 뭐 탐색은 BFS를 쓰거나 DFS를 쓰거나 상관없긴 한데, 이 코드의 제일 큰 차이점은 나처럼 탐색과정에서 지워지는 노드쪽은 제외후 탐색한것이 아니라, 에초에 그래프를 구성할때부터 삭제되는 노드와 그 부모노드의 간선을 끊어버림으로써, 탐색과정을 더욱 간결하게 만들었다. 이편이 BFS와 DFS의 정석적인 풀이가 아닌가 싶다.

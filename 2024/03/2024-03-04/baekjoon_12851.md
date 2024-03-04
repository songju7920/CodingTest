## 백준 12851번 숨바꼭질 2

### 문제 해결과정

- 문제 분류 : BFS
- 반환해야 하는 값 : 가장 빠르게 동생의 위치에 도달할때의 시간과, 가장 빠른 시간 안에 동생의 위치로 갈 수 있는 경우의 수를 구하여라
- 풀이과정
  1. BFS를 사용하여 탐색한다
  2. 만약 N == K라면 바로 탐색을 종료한다
  3. 만약 이미 목적지에 도달한 기록이 있고, 그 기록의 이동수보다 현재 이동수가 많다면 해당 탐색을 건너뛴다
  4. 이동한 위치가 0보다 크고 배열의 길이보다 작다면 다음을 실행하라:
     1. 만약 탐색을 안한 위치거나 지금 탐색이 과거에 한 탐색보다 시간이 적거나 같게 걸린다면 큐에 넣는다
     2. 만약 다음 위치가 목적지의 위치고, 거기에 도달한 기록과 시간이 같다면 답 카운트를 1올린다.
  5. 결과를 출력한다

### 풀이 코드

```python
from collections import deque

N, K = map(int, input().split())
maxLen = max(N, K) * 2
graph = [0] * maxLen
movement = [1, -1]

def BFS(start):
  answer = 0
  queue = deque([start])

  if K == N:
    return 1

  while queue:
    pos = queue.popleft()

    if graph[pos] + 1 > graph[K] and graph[K] != 0:
      continue

    # 앞뒤 +1, -1 이동
    for move in movement:
      npos = pos + move
      if 0 <= npos < maxLen:
        if graph[npos] == 0 or graph[pos] + 1 <= graph[npos]:
          graph[npos] = graph[pos] + 1
          queue.append(npos)
        if npos == K and graph[npos] == graph[pos] + 1:
          answer += 1

    # 현재 위치 두배 위치로 이동
    npos = pos * 2
    if 0 <= npos < maxLen:
      if graph[npos] == 0 or graph[pos] + 1 <= graph[npos]:
        graph[npos] = graph[pos] + 1
        queue.append(npos)
      if npos == K and graph[npos] == graph[pos] + 1:
        answer += 1

  return answer

answer = BFS(N)
print(graph[K])
print(answer)
```

코드 시간복잡도 (빅오) : O(N)

한줄 회고 : 이번 문제는 딱히 어려운점은 없었지만, 경우에수를 구하는 것이 생각보다 까다로웠다.

### 다른사람의 풀이

```python
import sys
from collections import deque
input=sys.stdin.readline

#가지수를 저장하는 방법..

def bfs(N):
    que=deque()
    que.append(N)
    ways[N]=1
    while que:
        a=que.popleft()
        for i in (a+1,a-1,2*a):

            if 0<=i<=100000:
                if Time[i]==0:
                    Time[i]=Time[a]+1
                    que.append(i)
                    ways[i]+=ways[a]

                elif Time[i]==Time[a]+1:
                    ways[i]+=ways[a]

N,K=map(int,input().split())

#시간과 가지수
Time=[0]*100001
ways=[0]*100001

if N<K:
    bfs(N)
    print(Time[K])
    print(ways[K])
elif N==K:
    print(0)
    print(1)
else:
    print(N-K)
    print(1)
```

이 풀이는 쓸대없는 반복도 줄였고, ways라는 배열을 추가하여 가독성도 높혔다
실제로 이 코드는 112ms정도를 소요하여, 164ms를 소요한 내 코드보다 훨씬 효율이 좋은것이다.
코드 정리를 조금만 하면 정말 완벽할것 같은 코드이다.

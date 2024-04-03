## 프로그래머스 10451번 순열 사이클

### 문제 해결과정

- 문제 분류 : 그래프 이론, 탐색
- 반환해야 하는 값 : 순열사이클의 개수를 구하여라
- 풀이과정
  1. 배열로 입력을 변환한다
  2. 해당 배열을 그래프로 취급, 그래프 탐색을 사용하여 탐색한다
  3. 탐색한 수를 구하여라

### 풀이 코드

```python
from collections import deque

T = int(input())

def BFS(start, graph, visit):
    next = start

    while next != -1:
        visit[next] = True
        if visit[graph[next]]:
            next = -1
        else:
            next = graph[next]

for _ in range(T):
    answer = 0
    N = int(input())
    numbers = [0] + list(map(int, input().split()))
    visit = [0] * (N + 1)

    for i in range(1, N + 1):
        if not visit[i]:
            BFS(i, numbers, visit)
            answer += 1

    print(answer)
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 그냥 평범한 탐색문제였다.

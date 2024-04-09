## 백준 28291번 **레드스톤**

### 문제 해결과정

- 문제 분류 : BFS
- 반환해야 하는 값 : 레드스톤 램프가 모두 켜질 수 있는가?
- 풀이과정
  1. 각자 입력을 받으며, 다음과 같은 과정을 거친다
  - 레드스톤 블록의 경우
    그래프에 해당 위치를 2로 표시함으로써, 해당 위체에 블록이 있다는걸 표시한다.
    방문 배열(전력 표시 배열)에 해당 위치의 전력을 16으로 설정한다
    StartPoint 배열에 해당 위치를 추가한다.

  - 레드스톤 램프의 경우
    그래프에 해당 위치를 -1로 표시함으로써, 해당 위체에 램프가 있다는걸 표시한다.
    램프의 개수 카운트를 1 올린다

  - 레드스톤 가루의 경우
    그래프에 해당 위치를 1로 표시함으로써, 해당 위체에 가루가 있다는걸 표시한다.
  2. 탐색을 시작하면, 다음과 같은 과정을 거친다.
     1. StartPoint배열을 queue로 만든다.
     2. movement 배열에 이동방향 (상하좌우)에 대한 좌표 이동값을 적는다
     3. queue가 비어있지 않은동안 다음 과정을 반복한다.
        1. queue에서 하나를 dequeue하여서 가져온다.
        2. 만약, 현재 있는 위치가 램프들중 하나의 자리고, 공급되는 전력이 있다면, answer의 값을 1 올리고 해당 반복을 건너뛴다.
        3. 이동 방향으로 갔을때, 위치들에 대하여 다음 동작을 실행한다

           만약, 배열의 범위를 벗어나지 않고, 해당 위치가 비어있는 공간이 아니며, 이전에 방문한적 없다면
           해당 좌표를 queue에 enqueue시키고, 방문 배열에 해당 위치가 가지게 되는 전력량을 표시한다.
  3. 만약 answer와 lampCnt의 개수가 같다면 success를, 아니면 failed를 출력하고 프로그램을 종료한다.

### 풀이 코드

```python
from collections import deque

W, H = map(int, input().split())

graph = [[0] * W for _ in range(H)]
visit = [[0] * W for _ in range(H)]
startPoint = []
lampCnt = 0

for i in range(int(input())):
  block_type, x, y = input().split()
  x, y = int(y), int(x)

  if block_type == "redstone_block":
    startPoint.append([x, y])
    graph[x][y] = 2
    visit[x][y] = 16
  elif block_type == "redstone_dust":
    graph[x][y] = 1
  elif block_type == "redstone_lamp":
    lampCnt += 1
    graph[x][y] = -1

def BFS(startPoints):
  movement = [[1, 0], [-1, 0], [0, 1], [0, -1]]
  queue = deque(startPoints)
  answer = 0

  while queue:
    x, y = queue.popleft()

    if graph[x][y] == -1 and visit[x][ey] > 0:
      answer += 1
      continue

    for mx, my in movement:
      nx, ny = x + mx, y + my
      if 0 <= nx < H and 0 <= ny < W and graph[nx][ny] != 0 and visit[nx][ny] == 0:
        queue.append([nx, ny])
        visit[nx][ny] = visit[x][y] - 1

  return answer

print("success" if BFS(startPoint) == lampCnt else "failed")
```

한줄 회고 : 코드가 좀 더럽고 길게 짜져서 많이 아쉽다.

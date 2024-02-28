## 백준 1027번 고층 건물

### 문제 해결과정

- 문제 분류 : 기하학, ccw 알고리즘, 브루트포스 알고리즘
- 반환해야 하는 값 : 건물의 높이가 주어졌을때, 다른 건물들을 최대한 많이 볼 수 있고,
- 풀이과정
  1. 처음 건물부터 탐색을 시작한다
  2. 현재건물 기준 왼쪽의 건물들이 다른 건물들에 교차되지 않는지 확인후, 교차되지 않는다면 결과값 +1
  3. 현재건물 기준 오른쪽의 건물들이 다른 건물들에 교차되지 않는지 확인후, 교차되지 않는다면 결과값 +1
  4. 결과값중 제일 큰 값 출력하기

### 풀이 코드

```python
import sys
input = sys.stdin.readline

N = int(input())
buildings = list(map(int, input().split()))
answers = []

def ccw(a, b, c):
  x1, y1 = a
  x2, y2 = b
  x3, y3 = c

  return (x1 * y2 + x2 * y3 + x3 * y1) - (y1 * x2 + y2 * x3 + y3 * x1)

for i in range(N):
  result = 0

  # 현재 건물 기준 왼쪽 탐색
  for j in range(0, i):
    for k in range(j + 1, i):
      if ccw([j, buildings[j]], [i, buildings[i]], [k, buildings[k]]) * ccw([j, buildings[j]], [i, buildings[i]], [k, 0]) <= 0:
        result -= 1
        break
    result += 1

  # 현재 건물 기준 오른쪽 탐색
  for j in range(i + 1, N):
    for k in range(i + 1, j):
      if ccw([i, buildings[i]], [j, buildings[j]], [k, buildings[k]]) * ccw([i, buildings[i]], [j, buildings[j]], [k, 0]) <= 0:
        result -= 1
        break
    result += 1

  answers.append(result)

print(max(answers))
```

코드 시간복잡도 (빅오) : O(n^3)

한줄 회고 : ccw 알고리즘을 처음 접했는데, 생각보다 유용하고 신기한 알고리즘이였다.

### 새로 알게된점

- CCW 알고리즘
  ![Untitled](https://velog.velcdn.com/images/yuz413/post/5d8dcb4d-53ce-4ffc-aad3-8376436e0b63/image.png)
  위에 보이는 그림처럼, 3점의 위치 관계를 파악하는 알고리즘이다.
  세 점이 시계방향으로 위치하면 음수를, 반시계방향으로 위치해 있다면 양수를, 직선일땐 0을 반환한다.
  CCW 알고리즘은 내부적으로 신발끈 공식을 사용한다. CCW알고리즘의 기본적인 수식은 다음과 같다:
  (x1 _ y2 + x2 _ y3 + x3 _ y1) - (y1 _ x2 + y2 _ x3 + y3 _ x1)
  ![Untitled](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2Flrykh%2FbtqIpvKjiQT%2F4hYKRhnXfGkj0HNMp6uWd0%2Fimg.png)
  CCW 알고리즘을 사용하면, 선분의 교차 여부를 판단 가능하다.
  C → D → A의 위치관계를 파악하면, 반시계방향으로 양수가 반환된다.
  C → D → B의 위치관계를 파악하면, 시계방향으로 음수가 반환된다.
  즉, CCW(C, D, A) \* CCW(C, D, B) < 0 라면 두 선분이 교차한다고 판단 가능하다.
  사진 출처:
  [CCW 알고리즘 (선분 교차 판별) - 코딩못하는사람](https://cantcoding.tistory.com/12)
  [CCW (Counter Clockwise) - yuz413.log](https://velog.io/@yuz413/CCW-Counter-Clockwise)

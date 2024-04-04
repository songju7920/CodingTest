## 백준 1193번 **분수찾기**

### 문제 해결과정

- 문제 분류 : 수학, 구현
- 반환해야 하는 값 : 지그제그 몽양으로 분수 배열을 순환할때,N번째로 탐색하는 분수를 찾는다.
- 풀이과정
  1. 만약 이번줄 탐색에서 N 위치에 도달하지 않는다면, 방향 전환 + 이번줄 탐색을 이동방향에 이번줄의 분수 개수만큼 곱해 더하여 처리하기
     예를들어서 1, -1으로 이동해야하고 이번줄의 분수 개수가 3개라면 3, -3을 더해 처리
  2. 만약 N위치에 도달하지 않았다면, 남은 분수만큼 현재 이동 방향으로 이동하여 찾기.

### 풀이 코드

- 처음 시도했던 코드 (시간초과)

```python
N = int(input())

numerator, denominator = 1, 1
move = [[-1, 1], [1, -1]]
direction = 0

for _ in range(1, N):
    mx, my = move[direction]
    numerator += mx
    denominator += my

    if numerator == 0:
        numerator = 1
        direction = (direction + 1) % 2

    if denominator == 0:
        denominator = 1
        direction = (direction + 1) % 2

print('%d/%d' %(numerator, denominator))
```

- 정답으로 처리된 코드

```python
N = int(input())

numerator, denominator = 1, 1
move1 = [[1, -1], [-1, 1]]
move2 = [[0, 1], [1, 0]]
direction = 0
cnt = 1
temp = 1

while temp + cnt + 1 < N:
    mx, my = move2[direction]
    numerator += mx
    denominator += my

    mx, my = move1[direction]
    numerator += mx * cnt
    denominator += my * cnt

    direction = (direction + 1) % 2

    cnt += 1
    temp += cnt

if temp < N:
    mx, my = move2[direction]
    numerator += mx
    denominator += my
    temp += 1

while temp < N:
    mx, my = move1[direction]
    numerator += mx
    denominator += my

    temp += 1



print('%d/%d' %(numerator, denominator))
```

한줄 회고 : 이 문제는 푸는데 굉장히 오래걸린 문제로, 구현방법에 애를 먹은 문제였다.

### 다른사람의 풀이

```python
n = int(input())

cnt = 0 #현재까지 온 분수 갯수
line = 0 #현재 줄

# n번째 위치가 존재하는 '줄' 찾기
while n > cnt:
    line += 1 #1,2,3,4
    cnt += line #1 + 2 + 3 +...

# 현재 줄에서 n의 위치까지의 거리
dis = cnt - n

# 해당 줄이 짝수면: 1 2,  홀수면: 2 1임
if line % 2 == 0:
    front = line - dis #이렇게 할 수 있는 이유는 우리는 해당 줄 가장 끝에 있어서다.
    back = dis +1
else:
    front = dis + 1
    back = line - dis

print('%d/%d'%(front,back))
```

코드 로직이 진짜 깔끔하다. 이런 방법으로 구현을 할 수가 있구나..

아마 난 수학적 사고력이 지금 너무 부족한것 같다. 이렇게 쉬운 문제를 저렇게 어려운 로직으로 풀다니.. 앞으로 수학 문제를 좀 많이 풀어봐야 겠다.

### 새로 알게된점

새로 알게된 알고리즘, 코드, 방식 정리

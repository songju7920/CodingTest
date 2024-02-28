# 18110 beakjoon

생성일: 2024년 1월 11일 오전 10:09

## 백준 18110번 Solved.ac

### 문제 해결과정

- 문제 분류 : 정렬, 수학
- 반환해야 하는 값 : 주어진 값의 30% 절사평균
- 풀이과정
    1. N을 입력받는다
    2. N의 15%를 구한뒤 반올림한다
    3. 수들을 입력받은뒤 정렬, 앞뒤에서 2번에서 구한 값만큼 뺀다
    4. 만약 N == 0이라면 0을 리턴
    5. 아니라면 3번에서 구한 수들의 평균을 계산해서 출력

### 풀이 코드

```jsx
import sys
input = sys.stdin.readline
EPS = 1e-9

N = int(input())
percent = round(N * 15 / 100 + EPS)

ratings = sorted([int(input()) for _ in range(N)])[percent: N - percent]

if N == 0: 
  print(0)
else:
  print(round(sum(ratings) / len(ratings) + EPS))
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 이 문제는 **round-to-nearest-even**이란 개념을 처음 본 문제라 정말 고생했다.

### 새로 알게된점

- Round-to-nearest-even(오사오입)
    
    이 식은 어떤 수를 반올림 했을때, 수가 N.5라면 앞이 짝수면 내림, 앞이 홀수면 올림하는 수학식이다. 예를 들어 2.5를 반올림하면 2가되고, 3.5를 반올림하면 4가 되는것이다.
    
    이러한 방식은 Python에 적용되어 있으며, 이를 피하기 위해 매우 작은 값을 더해 0.5를 감지하지 못하도록 만든다.
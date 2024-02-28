## 백준 12865번 **평범한 배낭**

### 문제 해결과정

- 문제 분류 : DP, 1-0 배낭문제
- 반환해야 하는 값 : 배낭에 넣을 수 있는 물건들의 가치의 최댓값
- 풀이과정
    1. 풀이과정

### 풀이 코드

```jsx
stuffCnt, limit = map(int, input().split())

stuffs = [[0, 0]] + [list(map(int, input().split())) for _ in range(stuffCnt)]

DPTable = [[0 for _ in range(limit + 1)] for _ in range(stuffCnt + 1)]

for i in range(1, stuffCnt + 1):
  for j in range(1, limit + 1):
    sw, sv = stuffs[i]
    if j < sw: DPTable[i][j] = DPTable[i - 1][j]
    else: DPTable[i][j] = max(DPTable[i - 1][j], DPTable[i - 1][j - sw] + sv)

print(DPTable[stuffCnt][limit])
```

코드 시간복잡도 (빅오) : O(n^2)

한줄 회고 : 배낭문제 알고리즘의 대표적인 문제이다.

### 새로 알게된점

- 1-0 배낭문제 알고리즘
    
    ![Untitled](https://velog.velcdn.com/images/dh1010a/post/b4b22cfc-b556-4c17-a50e-33941c251e7f/image.png)
    
    그림 출처: ([https://velog.io/@dh1010a/알고리즘-배낭문제-Knapsack-Problem](https://velog.io/@dh1010a/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%B0%B0%EB%82%AD%EB%AC%B8%EC%A0%9C-Knapsack-Problem))
    
    위 그림처럼, 2차원 배열로 DP를 표현하여 구현 가능하다. 간단하지만, 조금 응용하면 파악하기 힘든지라 앞으로 공부가 더 필요해보인다.
# Programers_12913

## 프로그래머스 12913번 땅따먹기

### 문제 해결과정

- 문제 분류 : DP
- 반환해야 하는 값 : 바닥까지 내려갈때, 얻을 수 있는 가장 큰 값
- 풀이과정
    1. DPTable 생성 및 초기화
    2. [1, 0]부터 [n, 3]까지 다음 내용 실행
        1. 윗줄중 자신과 같은 열은 건너뛰고 탐색
        2. 윗줄에서 찾은 값중 제일 큰값 + 자신의 점수를 해서 DP에 저장
    3. 맨 밑줄에서 제일 큰 값 찾기

### 풀이 코드

```python
def solution(land):
    DpTable = [[0] * 4 for _ in range(len(land))];
    DpTable[0] = land[0]
    
    for i in range(1, len(land)):
        for j in range(4):
            results = []
            for k in range(4):
                if k == j: continue
                results.append(DpTable[i - 1][k])
            DpTable[i][j] = max(results) + land[i][j]
        
    
    return max(DpTable[len(land) - 1]);
```

코드 시간복잡도 (빅오) : O(n + 4^2)

한줄 회고 : 그냥 평범한 DP 문제로, 쉬운 난이도였다. 아쉬웠던 점은, 코드가 조금 더럽다는것.

### 다른사람의 풀이

```python
def solution(land):

    for i in range(1, len(land)):
        for j in range(len(land[0])):
            land[i][j] = max(land[i -1][: j] + land[i - 1][j + 1:]) + land[i][j]

    return max(land[-1])
```

리스트 슬라이싱. 정말 기발한 풀이법이다. 파이썬의 list 기능을 100% 활용한 기법이라 할 수 있다..

또한, DP 테이블을 생성하지 않았는데.. 아마 이경우가 시간복잡도는 더 적게들지 않을 것 같다
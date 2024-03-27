# [PCCP 기출문제] 1번 / 붕대 감기

## 프로그래머스 250137번 붕대 감기

### 문제 해결과정

- 문제 분류 : 시뮬레이션
- 반환해야 하는 값 : 몬스터의 공격이 끝났을때의 HP. 만약 도중에 죽는다면 -1 Return
- 풀이과정
  1. 1초부터 마지막 공격시의 시간까지 for문 실행
  2. 만약 공격을 하는 시간이면 채력 깎고 연속 성공 카운트 초기화
  3. 공격을 안하는 시간이면 1초당 회복량 추가해주고 연속 성공 카운트 += 1
  4. 만약 일정 기간동안 연속 성공에 성공했다면 보너스 채력 올려줌
  5. 만약 HP가 0이하로 떨어지면 종료
  6. 만약 최대 채력보다 현재 채력이 높으면 최대채력으로 채력 낮추기

### 풀이 코드

```python
def solution(bandage, health, attacks):
    maxHealth = health
    attackIdx = 0
    healCount = 0

    for i in range(1, attacks[-1][0] + 1):
        if attacks[attackIdx][0] == i:
            health -= attacks[attackIdx][1]
            attackIdx += 1
            healCount = 0
        else:
            healCount += 1
            health += bandage[1]

        if healCount == bandage[0]:
            health += bandage[2]
            healCount = 0

        if health <= 0: break
        if health > maxHealth: health = maxHealth

    return -1 if health <= 0 else health
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 이 문제는 그냥 평범한 시뮬레이션 문제였다

### 다른사람의 풀이

```python
def solution(bandage, health, attacks):
    hp = health
    start = 1
    for i, j in attacks:
        hp += ((i - start) // bandage[0]) * bandage[2] + (i - start) * bandage[1]
        start = i + 1
        if hp >= health:
            hp = health
        hp -= j
        if hp <= 0:
            return -1
    return hp
```

이 풀이는 시간을 내 코드보다 더 줄인 예시로, 공격을 안받을때의 시간을 스킵하는 방법을 사용하였다.

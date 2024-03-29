# Programers_43165

## 프로그래머스 43165번 타겟 넘버

### 문제 해결과정

- 문제 분류 : BFS/DFS
- 반환해야 하는 값 : 주어진 숫자들을 더하거나 빼서 타겟 넘버가 되는 경우의 수를 구하여라
- 풀이과정
    1. BFS를 사용하여, 더하거나 빼거나를 그래프로 취급, 똑같은 로직을 사용하여 탐색한다.

### 풀이 코드

```python
from collections import deque

def solution(numbers, target):
    answer = 0
    actions = [1, -1]
    
    queue = deque([[numbers[0], 0], [numbers[0] * -1, 0]])
    
    while queue:
        num, idx = queue.popleft()
        idx += 1
        
        if idx == len(numbers) and num == target:
            answer += 1
        elif idx < len(numbers):
            for action in actions:
                queue.append([num + numbers[idx] * action, idx])
    
    return answer
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 이 문제는 DFS/BFS의 응용 문제였다. DFS/BFS 이론에 대하여 익숙하면 쉽게 풀 수 있었다.

### 다른사람의 풀이

```python
from itertools import product
def solution(numbers, target):
    l = [(x, -x) for x in numbers]
    s = list(map(sum, product(*l)))
    return s.count(target)
```

굉장히 흥미로웠던게, 조합, 순열을 이용한 풀이였는데 매우 흥미로웠다. DFS/BFS를 사용하지도 않고 풀 수 있음을 알았다.
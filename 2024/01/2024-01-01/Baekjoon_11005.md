## 백준 11005번 진법 변환 2

### 문제 해결과정

- 풀이 언어: Python
- 문제 분류 : 수학, 구현
- 반환해야 하는 값 : 숫자가 주어졌을때, 해당 숫자를 N진수로 변환한값을 출력하라
- 풀이과정
    1. N이 B보다 클동안 반복
        1. N을 B로 나눈 나머지 값을 진수 표기법에 맞게 변환해서 result에 추가
        2. N // B를 N의 값으로 설정
    2. 남은 N을 진수 표기법에 맞게 변환해서 result에 추가
    3. 결과를 뒤집어서 출력

### 풀이 코드

```python
alpabets = '0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ'
result = ''

[N, B] = map(int, input().split())
while N >= B:
  result += alpabets[N % B]
  N //= B
result += alpabets[N]

print(''.join(list(reversed(result))))
```

코드 시간복잡도 (빅오) : O(N)

한줄 회고 : 아 성능과 가독성을 고려하지 못해 코드가 매우 더러워 아쉽다.

### 다른사람의 풀이

```jsx
import string

n, base = map(int, input().split())

tmp = string.digits + string.ascii_lowercase
def convert(n, base):
    q, r = divmod(n, base)
    if q == 0:
        return tmp[r]
    else:
        return convert(q, base) + tmp[r]
    
print(convert(n, base).upper())
```

이분은 기본적으로 내장 함수들을 잘 사용하시고, 재귀함수의 활용도가 매우 뛰어나다. 한마디로 가독성이 매우 좋으며, 성능도 좋은 코드이다.

### 새로 알게된점

- string.digits & string.ascii_lower/uppercase
    
    ```python
    string.digits #123456789
    string.ascill_uppercase #ABCDEFGHIJKLMNOPQRSTUVWXYZ
    ```
    
- divmod
    
    왼쪽에는 나눗셈의 몫, 오른쪽에는 나머지를 반환해주는 내장함수
    
    ```python
    divmod(12,4) -> (12 // 4, 12 % 4) -> (3, 0)
    ```
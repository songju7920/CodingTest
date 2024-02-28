## 프로그래머스 77884번 약수의 개수와 덧셈

- 문제 풀이 과정
  1. left에서 right숫자 하나하나씩 추출해 반복한다.
     1. 이 수의 약수를 구한다.
     2. 짝수이면 더하고, 홀수면 뺸다.

풀이 코드 :

```jsx
function solution(left, right) {
  var answer = 0;
  for (let i = left; i <= right; i++) {
    let measure = 1;
    for (let j = 1; j <= i / 2; j++) measure += i % j == 0 ? 1 : 0;
    if (measure % 2 == 0) answer += i;
    else answer -= i;
  }
  return answer;
}
```

이 문제는 간단한 로직만 세우면 매우 쉽게 해결할수 있는 문제였다.

- 다른사람의 풀이
  ```jsx
  function solution(left, right) {
    var answer = 0;
    for (let i = left; i <= right; i++) {
      if (Number.isInteger(Math.sqrt(i))) {
        answer -= i;
      } else {
        answer += i;
      }
    }
    return answer;
  }
  ```
  이 코드는 정말 시간 효율성이 나의 풀이보다 높다. 단순히 계산만 함으로써 약수의 개수가 짝수인지 홀수인지 알아냈다.
- 새로 알게된점
  수식에 대해 새로 알게되었는데, 수의 제곱근이 정수라면 그 수는 약수의 개수가 홀수이고, 정수가 아니라면 약수의 개수가 짝수라는것을 알수 있었다.

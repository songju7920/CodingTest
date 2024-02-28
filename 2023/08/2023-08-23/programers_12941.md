## 프로그래머스 12941번 최소값 만들기

- 문제 해결과정
  - 반환해야 하는 값 : 배열의 값들을 하나씩 곱하여 더해서 만들어지는 수중 가장 작은 수를 출력하라.
  1. 오름차순, 내림차순으로 정렬한다.
  2. 배열 2개를 앞에서부터 서로 곱해 더한다.

풀이 코드 :

```jsx
function solution(A, B) {
  var answer = 0;

  A.sort((a, b) => a - b);
  B.sort((a, b) => b - a);

  for (let i = 0; i < A.length; i++) {
    answer += A[i] * B[i];
  }

  return answer;
}
```

이 문제는 간단한 문제로, 문제 설명만 봐도 쉽게 풀수 있는 문제였다.

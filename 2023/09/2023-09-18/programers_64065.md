## 프로그래머스 64065번 튜플

- 문제 해결과정
  - 반환해야 하는 값 : s가 표현하는 튜플을 배열에 담아 return
  1. 튜플을 배열로 분리
  2. answer에 포함되있지 않은 element라면 push
  3. answer 요소들을 number로 바꿔서 return

풀이 코드 :

```jsx
function solution(tuple) {
  var answer = [];
  tuple = tuple
    .slice(2, tuple.length - 2)
    .split(/},{/)
    .sort((a, b) => a.length - b.length);

  tuple.map((arr) => {
    arr = arr.split(",");
    arr.map((element) => {
      if (answer.indexOf(element) == -1) answer.push(element);
    });
  });

  return answer.map((a) => Number(a));
}
```

이 문제는 정규표현식만 잘 활용한다면 쉬운 문제였다

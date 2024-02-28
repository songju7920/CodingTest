## 프로그래머스 42748번 K번째

- 문제 해결과정
  - 반환해야 하는 값 : 배열열을 정해진 시작지점과 종료지점을 기준으로 잘라서 목표지점에 있는 요소 뽑아서 배열어 담기.
  1. commends 순회
  2. commend 시작지점, 종료지점, 타겟 인덱스 확인
  3. 배열 자른후 오름차순으로 정렬
  4. 타겟 인덱스의 요소 가져오기

풀이 코드 :

```jsx
function solution(array, commands) {
  let answer = [];
  commands.map((commend) => {
    let [start, end, target] = commend;
    answer.push(array.slice(start - 1, end).sort((a, b) => a - b)[target - 1]);
  });
  return answer;
}
```

이 문제는 조금만 생각하면 풀수 있는 아주 간단한 문제였다.

- 다른사람의 풀이
  ```tsx
  function solution(array, commands) {
    return commands.map((command) => {
      const [sPosition, ePosition, position] = command;
      const newArray = array
        .filter(
          (value, fIndex) => fIndex >= sPosition - 1 && fIndex <= ePosition - 1
        )
        .sort((a, b) => a - b);

      return newArray[position - 1];
    });
  }
  ```
  이 사람은 filter을 사용하여 요소를 뽑아낸뒤 sort를 하여 리턴하는 방식으로 풀었다.

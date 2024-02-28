## 프로그래머스 42889번 실패율

- 문제 해결과정
  - 반환해야 하는 값 : 영어로 된 숫자들을 숫자로 바꾸어 반환하라
  1. answer를 초기화시킨다
  2. N만큼 다음 조건을 반복한다
     1. stages에서 i만 같은 요소를 뽑아내서 그 단계에 있는 플래이어만 추출한다.
     2. 실패율 배열에 실패율을 계산하여 넣는다.
  3. answer를 초기화 배열에 기반하여 정렬한다.

풀이 코드 :

```jsx
function solution(N, stages) {
  let failureRates = [];
  let answer = [];
  let players = stages.length;

  for (let i = 1; i <= N; i++) {
    answer.push(i);
  }

  for (let i = 1; i <= N; i++) {
    let leftPlayers = stages.filter((stage) => stage == i).length;
    failureRates.push(leftPlayers / players);
    players -= leftPlayers;
  }

  answer.sort((a, b) => {
    let idxA = answer.indexOf(a);
    let idxB = answer.indexOf(b);

    return failureRates[idxB] - failureRates[idxA];
  });

  return answer;
}
```

이 문제는 마지막 정렬에서 굉장히 애를 먹었던 문제였다.

- 다른사람의 풀이
  ```jsx
  function solution(N, stages) {
    let result = [];
    for (let i = 1; i <= N; i++) {
      let reach = stages.filter((x) => x >= i).length;
      let curr = stages.filter((x) => x === i).length;
      result.push([i, curr / reach]);
    }
    result.sort((a, b) => b[1] - a[1]);
    return result.map((x) => x[0]);
  }
  ```
  이 사람은 이차원 배열을 사용하여 효율적으로 풀었다. 정말 코드가 깔끔하고 조금만 읽어보면 이해할수 있을정도로 가독성이 좋은 코드이다. 나도 다음에 비슷한 문제를 마주치면 2차원 배열로 풀려는 시도를 해봐야겠다.

## 프로그래머스 42586번 **기능개발**

- 문제 해결과정
  - 반환해야 하는 값 : 문자열 my_string과 문자 letter이 매개변수로 주어집니다. my_string에서 letter를 제거한 문자열을 return하라
  1. 개발 일수를 (100-progress)/spead[i]를 올림 하여 구한다.
  2. 모든 개발 프로그램 개발 소요시간을 위 식을 이용해 구한다.
  3. Days배열에 아무것도 없을때까지 아래내용 반복.
     1. Cnt 1로 초기화
     2. 만약 Day[0]이 뒤에 오는 Days의 요소보다 크다면 해당 요소를 삭제후 Cnt++
     3. 아니라면 answer배열에 Cnt 넣고 반복문 처음으로 이동

풀이 코드 :

```jsx
function solution(progresses, speeds) {
  let answer = [],
    Days = [],
    rep = 0;

  //개발
  progresses.forEach((progress) => {
    Days.push(Math.ceil((100 - progress) / speeds[rep]));
    rep++;
  });

  //배포
  while (Days[0] != null) {
    let Cnt = 1;
    let Day = Days.shift();
    while (1) {
      if (Day >= Days[0]) {
        Days.shift();
        Cnt++;
      } else {
        answer.push(Cnt);
        break;
      }
    }
  }
  return answer;
}
```

이번 문제는 큐 자료구조를 사용해야 했던 문제이다. JS에서 큐의 enqueue와 dequeue를 js에서 push와 shift함수를 이용해 구현하였다.

다른사람의 코드 :

```jsx
function solution(progresses, speeds) {
  let answer = [0];
  let days = progresses.map((progress, index) =>
    Math.ceil((100 - progress) / speeds[index])
  );
  let maxDay = days[0];

  for (let i = 0, j = 0; i < days.length; i++) {
    if (days[i] <= maxDay) {
      answer[j] += 1;
    } else {
      maxDay = days[i];
      answer[++j] = 1;
    }
  }

  return answer;
}
```

위 코드는 전체적인 로직 자체는 나의 코드와 비슷하나, forEach대신 map을 사용하여 시간복잡도를 작게 만들어 나의 코드보다 더 빠르게 처리할수 있다.

- 알게된점

  - forEach vs Map

    > forEach() — executes a provided function once for each array element
    >
    > => 배열요소마다 한 번씩 제공한 함수를 실행합니다.

    > map() — creates a new array with the results of calling a provided function on every element in the calling array.
    >
    > => 배열 내의 모든 요소 각각에 대하여 제공된 함수를 호출하고, 그 결과를 모아서 새로운 배열을 반환합니다.

    위 MDN의 정의로 볼때 제일 중요한 차이점은 map은 동일한 사이즈의 새로운 배열을 반환한다는 것이다.

  사용 예시 :

  ```tsx
  //forEach 사용 예시
  arr.forEach((num, index) => {
    return (arr[index] = num * 2);
  });

  // arr = [2, 4, 6, 8, 10]

  //map 사용 예시
  let doubled = arr.map((num) => {
    return num * 2;
  });

  // doubled = [2, 4, 6, 8, 10]
  ```

  또, 다른 차이점으로는 map함수가 대부분의 상황에서 forEach문보다 빠르다는 차이점도 존재한다.

  즉, 둘의 차이점은 다음 표로 정리할수있다.
  | 차이점 \ 함수 | forEach | map |
  | ------------- | ------------- | ------------- |
  | 속도 | 느리다 | 빠르다 |
  | 반환 | 입력된 배열로 | 새로운 배열로 |

  결론적으로는 왠만해서는 forEach대신 map을 사용하는것이 효율적이다.

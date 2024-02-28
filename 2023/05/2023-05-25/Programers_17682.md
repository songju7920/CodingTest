## 프로그래머스 17682 다트게임

- 문제 해결과정
  - 반환해야 하는 값 : 0~10의 정수와 문자 S, D, T, \*, #로 구성된 문자열이 입력될 시 총점수를 반환하는 함수를 작성하라.
  1. 정규표현식을 사용하여 데이터를 분리시킨다.
  2. dartData배열의 길이가 0 이상일때까지 반복한다.
     1. 보너스의 값에 따라 점수를 제곱시킨다
     2. 옵션에 따라 점수에 보너스를 부여하거나 감점시킨다.
  3. 결과를 도출한다.

풀이 코드 :

```jsx
function solution(dartResult) {
  let scores = [];
  let option;

  //데이터 분리
  let dartData = dartResult.match(/(\d+)|([A-Z]+)|(\W+)/g);
  while (dartData.length > 0) {
    let score = dartData.shift();
    let bonus = dartData.shift();
    if (dartData[0] == "*" || dartData[0] == "#") option = dartData.shift();
    else option = null;

    //점수 제곱
    switch (bonus) {
      case "S":
        scores.push(Number(score));
        break;
      case "D":
        scores.push(score * score);
        break;
      case "T":
        scores.push(score * score * score);
        break;
    }

    //옵션처리
    switch (option) {
      case "*":
        if (scores.length > 1) {
          let a = scores.pop() * 2;
          scores.push(scores.pop() * 2);
          scores.push(a);
        } else scores[0] *= 2;
        break;
      case "#":
        scores.push(scores.pop() * -1);
        break;
      case null:
        break;
    }
  }

  return scores.reduce((a, b) => a + b);
}
```

이 문제는 로직을 차근차근 세우고 전체적인 함수 사용법과 Js문법만 알고있다면 쉽게 풀수 있는 문제였다.

- 새로 알게된점
  - match함수
    정규표현식을 사용 하여 sort함수와 비슷하게 문자열을 분리하여 배열로 바꾸어주지만 sort와 다르게 분리점을 삭제하지않고도 분리가 가능하다.
    사용예시 :
    ```jsx
    arr = "1Two3Four5"
    let data = arr.match(/(\d+)|([A-Z]+)/);
    console.log(data) => [1, "Two", 3, "Four", 5]
    ```

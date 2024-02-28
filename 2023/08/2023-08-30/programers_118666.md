## 프로그래머스 118666번 성격 유형 검사하기

- 문제 해결과정
  - 반환해야 하는 값 : 설문의 선택지의 값과 사용자의 선택이 주어질때 성격유형을 도출하는 코드를 작성하라
  1. 4보다 작으면 값에따라 앞의 항목에 점수부여
  2. 4보다 크면 값에따라 뒤의 항목에 점수부여

풀이 코드 :

```jsx
//MBTI 데이터
const MBTI = {
  R: 0,
  T: 0,
  C: 0,
  F: 0,
  J: 0,
  M: 0,
  A: 0,
  N: 0,
};

function solution(survey, choices) {
  var answer = "";

  //MBTI 데이터 분류
  choices.forEach((choice, idx) => {
    if (4 > choice) {
      MBTI[survey[idx].split("")[0]] += 4 - choice;
    } else if (4 < choice) {
      MBTI[survey[idx].split("")[1]] += choice - 4;
    }
  });

  //MBTI 결정
  answer += MBTI.R < MBTI.T ? "T" : "R";
  answer += MBTI.C < MBTI.F ? "F" : "C";
  answer += MBTI.J < MBTI.M ? "M" : "J";
  answer += MBTI.A < MBTI.N ? "N" : "A";

  return answer;
}
```

이번 문제는 로직을 차근차근 생각해보면 쉽게 풀 수 있는 문제였다.

- 새로 알게된점
  변수값을 key값으로 사용하여 객체의 value값 선택하는법
  단순히 []로 변수를 감싸서 사용할수 있다.
  ```jsx
  const obj = {
  	key1 : value1;
  	key2 : value2;
  }

  let keyName = "key1";
  console.log(obj[keyName]) // value1
  ```

.

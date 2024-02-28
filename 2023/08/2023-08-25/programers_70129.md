## 프로그래머스 70129번 이진 변환 반복하기

- 문제 해결과정
  - 반환해야 하는 값 : 문자열이 1이 될때까지 문자열의 0을 지우고, 지운 문자열의 길이를 2진수로 변환후 위의 과정을 반복했을때, 길이를 2진수로 바꾼 횟수와 지운 0의 갯수를 배열에 담아서 return한다.
  1. s.length가 1보다 클때동안 다음을 반복한다.
     1. s를 배열로 바꾼다.
     2. 배열을 순회하면서 queue를 활용해 0을 제외시킨다
     3. 다시 문자열로 만든뒤 길이를 2진수로 전환한다.
  2. 배열을 리턴한다

풀이 코드 :

```jsx
function solution(s) {
  let answer = [0, 0];
  while (s.length > 1) {
    s = s.split("");

    let length = s.length;

    for (let i = 0; i < length; i++) {
      let num = s.shift();
      if (num == "1") {
        s.push(num);
      } else {
        answer[1]++;
      }
    }

    answer[0]++;
    s = s.length.toString(2);
  }

  return answer;
}
```

이 문제는 자료구조를 사용해 풀었던 문제였다. 로직을 생각하는데 조금 애를 먹었지만 조금만 생각하면 쉽게 풀수 있었다

- 다른사람의 풀이
  ```tsx
  function solution(s) {
    var answer = [0, 0];
    while (s.length > 1) {
      answer[0]++;
      answer[1] += (s.match(/0/g) || []).length;
      s = s.replace(/0/g, "").length.toString(2);
    }
    return answer;
  }
  ```
  이사람은 reduce와 match, 정규표현식을 사용하여 로직을 더 간단하게 구성하였다.

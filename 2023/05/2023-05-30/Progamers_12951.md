## 프로그래머스 12951번 JadenCase 문자열 만들기

- 문제 해결 과정
  - 반환해야 하는값 : s를 JadenCase로 바꾼 문자열을 리턴
  1. 문자열을 나눈다.
  2. 첫번째 숫자를 대문자로 만든다.
  3. words의 idx 1부터 마지막 idx까지 반복한다.
     1. words[i]가 공백이고 뒤에 오는 단어가 공백이나 undifined가 아니라면 대문자로 만들고 idx를 건너뛴다.
     2. words[i]가 공백이 아니라면 words[i]를 소문자로 만든다.

풀이 코드 :

```jsx
function solution(s) {
  let words = s.split("");
  words[0] = words[0].toUpperCase();

  for (let i = 1; i < words.length; i++) {
    if (words[i] === " ") {
      if (words[i + 1] != " " && words[i + 1] != undefined) {
        words[i + 1] = words[i + 1].toUpperCase();
        i++;
      }
      continue;
    }

    words[i] = words[i].toLowerCase();
  }
  return words.join("");
}
```

이 문제는 조건때문에 어려웠는데, 공백이 한번에 연속되서 나올수 있다는 조건을 처리하느라 힘들었던 문제였다.

- 다른사람의 풀이
  ```jsx
  function solution(s) {
    return s
      .split(" ")
      .map((v) => v.charAt(0).toUpperCase() + v.substring(1).toLowerCase())
      .join(" ");
  }
  ```
  이사람은 map함수를 이용하여 split함수로 분리한 s를 계산해 반환하였다. 앞으로 나도 이런 코드를 짤수있도록 노력해야겠다는 생각이 들었다.

## 프로그래머스 12909번 올바른 괄호

- 문제 해결 과정
  1. number 분리
  2. number배열 길이 0이 아닐때 동안 반복
     1. number 꺼냈을때 스택이 비어있는데 ‘)’라면 false 리턴
     2. 만약 ‘(’이 스택에 있으면 스택 pop
  3. 만약 스택이 안비어있다면 false 리턴

풀이코드 :

```jsx
function solution(s) {
  let stack = [];
  s = s.split("");

  for (let char of s) {
    if (char == ")" && stack.length == 0) return false;
    if (char == "(") stack.push(char);
    if (char == ")") stack.pop();
  }

  return stack.length == 0;
}
```

옛날에는 굉장히 어렵다고 느껴져 포기한 문제인데 지금 와서 풀어보니 쉽고 간단한 문제였다.

- 다른사람의 풀이
  ```jsx
  function solution(s) {
    let cum = 0;
    for (let paren of s) {
      cum += paren === "(" ? 1 : -1;
      if (cum < 0) {
        return false;
      }
    }
    return cum === 0 ? true : false;
  }
  ```
  이사람은 스택을 사용하지 않고 삼항연산자와 조건문만을 사용하여 풀이하였다.

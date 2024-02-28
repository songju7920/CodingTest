## 프로그래머스 42587번 프로세스

풀이 코드 :

```jsx
function solution(priorities, location) {
  let answer = 0;

  while (true) {
    let max = Math.max(...priorities);
    let first = priorities.shift();

    if (max == first) {
      answer++;
      if (location == 0) break;
      else location--;
    } else {
      priorities.push(first);
      if (location == 0) location = priorities.length - 1;
      else location--;
    }
  }

  return answer;
}
```

이 문제는 문제 해결 과정을 문제에 써놓았음에도 굉장히 어려웠던 문제였는데, 생각보다 너무 허무하게 풀려버려서 너무 아쉬웠다. 때문에 정확히 로직을 새운뒤 해결하지 못한것 같아서 풀었음에도 많이 찝찝했다. 다음부턴 꼭 로직 세우고, 차근차근 풀어봐야겠다고 생각했다.

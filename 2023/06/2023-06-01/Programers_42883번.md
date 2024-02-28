## 프로그래머스 42883번 큰 수 만들기

- 문제 해결 과정
  1. number 분리후 스택으로 변환
  2. number 뒤쪽에서 꺼내서 answer에 push
  3. 만약 다음 들어올 number값이 answer에 top값보다 크다면 answer.pop시키기
  4. answer를 합체해서 return

풀이코드 :

```jsx
function solution(number, k) {
  let answer = [];
  number = number.split("").reverse();

  if (k == 1) number.shift();

  while (number.length > 0) {
    answer.push(number.pop());
    while (answer[answer.length - 1] < number[number.length - 1] && k > 0) {
      answer.pop();
      k -= 1;
    }
  }

  return answer.join("");
}
```

이번 문제는 정말 풀면서 답답하고 화가 나기도 했던 내가 풀었던 문제중 제일 어려웠던 문제 같았다. 결국에는 푼 사람들의 힌트를 참고해 풀었는데, 이런곳에서도 자료구조를 사용해 풀수 있다는것이 매우 놀라웠다.

- 알게된점
  - stack이 queue보다 시간복잡도가 더 적다(최중요)
    자료구조 구조상 stack이 queue보다 시간복잡도가 작을수밖에 없다. stack은 꺼낼때 뒤에서 하나만 꺼내면 되지만, queue는 앞에껄 꺼낸뒤 자릿수를 하나씩 당겨 주어야 하기때문이다.

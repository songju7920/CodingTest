## 프로그래머스 160586번 **대충 만든 자판**

- 문제 해결과정
  - 반환해야 하는 값 : 입력해야하는 문자열과 키 배열이 주어졌을때, 문장을 완성할수 있으면 최소 입력횟수를 계산해서 배열에 담고, 완성할수 없다면 -1을 배열에 담아서 배열을 return
  1. targets를 순회한다.
  2. target을 배열로 분해후, 배열값에 접근한다.
  3. keymap에 target의 값들을 차례대로 비교해보며 제일 target의 글자와 일치하는 keymap에 서 target글자의 index를 찾는다.
  4. 만약 min에 변동이 없다면 배열에 -1을, 그렇지않다면 sum을 넣는다.
  5. 배열을 return한다.

풀이 코드 :

```jsx
function solution(keymap, targets) {
  var answer = [];
  targets.forEach((target) => {
    let sum = 0;
    target = target.split("");

    //target roop
    for (let i = 0; i < target.length; i++) {
      let min = 101;

      //keymap 순회하면서 index 찾기
      for (let j = 0; j < keymap.length; j++) {
        let idxOfKey = keymap[j].indexOf(target[i]);
        if (idxOfKey == -1) continue;
        min = idxOfKey < min ? idxOfKey : min;
      }

      if (min == 101) {
        sum = 0;
        break;
      } else {
        sum += min + 1;
      }
    }
    answer.push(sum == 0 ? -1 : sum);
  });
  return answer;
}
```

이 문제는 배열에 대한 이해, indexOf활용, 자료구조만 간단히 알고있으면 쉽게 풀수 있었다.

- 다른 사람의 풀이
  ```jsx
  function solution(keymap, targets) {
    const answer = [];
    const map = {};
    for (const items of keymap) {
      items
        .split("")
        .map(
          (item, index) =>
            (map[item] = map[item] < index + 1 ? map[item] : index + 1)
        );
    }
    for (const items of targets) {
      answer.push(
        items.split("").reduce((cur, item) => (cur += map[item]), 0) || -1
      );
    }
    return answer;
  }
  ```
  이 사람은 split과 map을 사용하여

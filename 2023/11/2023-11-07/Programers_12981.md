## 프로그래머스 12981번 **영어 끝말잇기**

### 문제 해결과정

- 문제 분류 : 구현
- 반환해야 하는 값 : 영어 끝말잇기에서 제일 첫번째로 탈락하는 사람의 번호와 몇 번째 차례에 탈락하는지 출력하라.

### 풀이 코드

```jsx
function solution(n, words) {
  let answer = [0, 0];
  let startsWith = "";
  let turn = 1;
  let idx = 0;

  for (let word of words) {
    if (idx != 0 && word[0] != startsWith) {
      return [(idx % n) + 1, turn];
    }
    if (words.indexOf(word) != idx) {
      return [(idx % n) + 1, turn];
    }
    startsWith = word[word.length - 1];
    if ((idx + 1) % n == 0) turn++;
    idx++;
  }

  return answer;
}
```

코드 시간복잡도 (빅오) : 사실상 O(n^2)에 가까움

한줄 회고 : 이 문제는 Lv.2치고는 매우 간단 했던 문제였다.

### 고찰

다른사람과 나의코드를 비교해보다가 내 코드를 약간 수정해 실험해봤더니

```jsx
function solution(n, words) {
  let answer = [0, 0];
  let startsWith = "";
  let turn = 1;
  let idx = 0;

  for (let word of words) {
    if ((idx != 0 && word[0] != startsWith) || words.indexOf(word) != idx) {
      return [(idx % n) + 1, turn];
    }
    startsWith = word[word.length - 1];
    if ((idx + 1) % n == 0) turn++;
    idx++;
  }

  return answer;
}
```

이 코드가 개선전 코드보다 10번 테스트 케이스에서 100ms정도 빠른 것을 포착했다.

한참 고민해보았다. “왜 기존 코드보다 이 코드가 더 빠를까?”

내 생각에서는 분명 조건문 안의 연산이 늘어나 느려질것이라 생각했다. 특히 indexOf 때문에 느려질 것이 분명해보였다.

그래서, 비슷한 상황으로 개인 IDE에서 코드를 실행해보았다.

```jsx
function test1(n, idx) {
  let words = [
    "tank",
    "kick",
    "know",
    "wheel",
    "land",
    "dream",
    "mother",
    "robot",
    "tank",
  ];
  if (1 == n || words.indexOf("robot") != idx) return;
  return;
}

console.log("조건문을 1개로 통합");

console.log("둘다 맞출경우");
console.time();
test1(1, 7); // 둘다 맞출경우
console.timeEnd();

console.log("앞을 틀릴 경우");
console.time();
test1(2, 7); // 앞을 틀릴 경우
console.timeEnd();

console.log("뒤를 틀릴 경우");
console.time();
test1(1, 2); // 뒤를 틀릴 경우
console.timeEnd();

function test2(n, idx) {
  let words = [
    "tank",
    "kick",
    "know",
    "wheel",
    "land",
    "dream",
    "mother",
    "robot",
    "tank",
  ];
  if (1 == n) return;
  if (words.indexOf("robot") != idx) return;
  return;
}

console.log("\n조건문을 2개로 분리");

console.log("둘다 맞출경우");
console.time();
test1(1, 7); // 둘다 맞출경우
console.timeEnd();

console.log("앞을 틀릴 경우");
console.time();
test1(2, 7); // 앞을 틀릴 경우
console.timeEnd();

console.log("뒤를 틀릴 경우");
console.time();
test1(1, 2); // 뒤를 틀릴 경우
console.timeEnd();
```

결과 :

```
조건문을 1개로 통합
둘다 맞출경우
default: 0.045ms
앞을 틀릴 경우
default: 0.003ms
뒤를 틀릴 경우
default: 0.001ms

조건문을 2개로 분리
둘다 맞출경우
default: 0.001ms
앞을 틀릴 경우
default: 0.004ms
뒤를 틀릴 경우
default: 0.004ms
```

결과를 보면 둘다 맞출경우 1개로 통합하는것이, 하나라도 틀릴 시 1개로 통합하는 것이 시간복잡도가 적다는 결론을 도출해 냈다. 즉, 결과적으로 보면 10번 테스트 케이스는 앞의 조건이나 뒤의 조건중 하나를 틀린 코드가 많았다고 생각되며, 평균을 도출 해보았을때, 조건문을 2개로 분리하는 것이 더 효율적이였다.

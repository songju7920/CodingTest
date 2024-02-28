## 프로그래머스 131127번 할인 행사

- 문제 해결과정
  - 회원등록시 정현이가 원하는 제품을 모두 할인 받을 수 있는 회원등록 날짜의 총 일수 return
  1. number의 총합을 구하기
  2. 할인 품목 배열의 길이 - number의 총합 + 1만큼 반복
     1. idx i부터 10길이만큼 배열 자르기
     2. 자른 배열을 순회하며 필요항목을 모두 포함하는지 확인하기
     3. 만약 모두 포함되면 answer 1증가
  3. answer 반환

풀이 코드 :

```jsx
function solution(wants, number, discount) {
  let answer = 0;
  let totalCnt = number.reduce((a, b) => a + b);

  for (let i = 0; i < discount.length - totalCnt + 1; i++) {
    let cnt = 0;
    let item = discount.slice(i, 10 + i);
    wants.forEach((want, idx) => {
      let itemCnt = item.filter((a) => a == want).length;
      if (number[idx] == itemCnt) cnt++;
    });
    if (cnt == wants.length) answer++;
  }
  return answer;
}
```

이 문제는 문제의 의도만 잘 파악하고 로직을 차근차근 세우기만 한다면 쉬운 문제였다.

- 다른 사람의 풀이

  ```jsx
  function solution(want, number, discount) {
    let count = 0;
    for (let i = 0; i < discount.length - 9; i++) {
      const slice = discount.slice(i, i + 10);

      let flag = true;
      for (let j = 0; j < want.length; j++) {
        if (slice.filter((item) => item === want[j]).length !== number[j]) {
          flag = false;
          break;
        }
      }
      if (flag) count += 1;
    }
    return count;
  }
  ```

  이분은 나의 로직과 약간 다르게 원하던 상품이 일정 원하는 수량 만큼 없다면 바로 반복문을 탈출하는 식으로 코드를 구성하였다. 이러면 확실히 나의 코드보다 시간복잡도가 줄어들것 같다.

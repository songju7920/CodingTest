## 프로그래머스 120956번 **옹알이(1)**

- 문제 해결과정
    - 반환해야 하는 값 :조카가 발음할 수 있는 단어의 개수를 return.
    1. 정규표현식으로 해당 발음들을 빈 문자열로 바꾸었을때, 빈문자열만 걸러내기.
    2. 걸러낸 배열 길이 Return

풀이 코드 :

```jsx
function solution(babbling) {
    let answer = babbling.filter(a => !(a.replaceAll(/aya|ye|woo|ma/g, "")));
    return answer.length
}
```

이 문제는 정규표현식만 알면 정말 쉬운 문제였다.
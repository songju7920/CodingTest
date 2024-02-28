## 프로그래머스 12903번 가운데 글자 가져오기

- 문제 해결과정
    - 반환해야 하는 값 : 단어 s의 가운데 글자를 반환하는 함수, solution을 설계하라
    1. 만약 문자열의 길이가 짝수면 가운데 2 글자를 answer에 추가한다.
    2. 아니면 문자열의 길이가 홀수면 가운데 글자를 answer에 추가한다.

풀이 코드 :

```jsx
function solution(s) {
    var answer = '';
    if(s.length % 2 == 0){
        answer = s[s.length/2 - 1]
        answer += s[s.length/2]
    }
    else answer = s[Math.floor(s.length/2)];
    return answer;
}
```

이번 문제는 기본적으로 쉬웠지만, 어려웠던 점을 뽑으라고 하면 문자열 길이가 홀수일때 Math.floor로 소수점자리를 없에야 했던것이였다.

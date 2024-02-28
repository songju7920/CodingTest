# Kakao 2021 신규 아이디 추천

생성일: 2023년 7월 10일 오후 4:44

## 프로그래머스 72410번 신규 아이디 추천

- 문제 해결과정
    - 반환해야 하는 값 : 주어진 규칙에 따라 아이디를 변형시키는 함수를 제작하여라.
1. 모든 글자들을 소문자로 변환한다
2. 문자, 특수문자 -, _, . 을 제외하고 모두 삭제
3. .이 2번이상 반복되는 모든 문자열을 .으로 변환
4. .으로 시작하거나 .으로 끝나는 .삭제
5. 공백이면 a넣어주기
6. 15번째 idx까지 자른후 마지막에 . 있다면 삭제
7. 3보다 작을경우 마지막 글자로 3글자 될때까지 채우기

풀이 코드 :

```jsx
function solution(new_id) {
    var answer = '';
    new_id = new_id.toLowerCase()
    .replaceAll(/[^\w\-\.]/g, "")
    .replaceAll(/\.{2,}/g, ".")
    .replace(/\.$/, "")
    .replace(/^\./, "");
    
    new_id = new_id == "" ? "a" : new_id;
    new_id = new_id.split('').splice(0, 15).reduce((a, b) => a + b).replace(/\.$/, "");
    while(new_id.length < 3) new_id += new_id[new_id.length - 1];
    return new_id;
}
```

이번 문제는 능숙한 정규표현식의 사용을 요구하던 문제였다.

- 다른사람의 풀이
    
    ```jsx
    const solution = (new_id) => {
        const id = new_id
            .toLowerCase()
            .replace(/[^\w\d-_.]/g, '')
            .replace(/\.{2,}/g, '.')
            .replace(/^\.|\.$/g, '')
            .padEnd(1, 'a')
            .slice(0, 15)
            .replace(/^\.|\.$/g, '')        
        return id.padEnd(3, id[id.length-1])
    }
    ```
    
    padStart를 이용하여 부족한 부분을 채워 넣은 것이 정말 인상 깊었다. 그 하나로 코드의 가독성도 엄청나게 올라갔으며, 시간복잡도도 줄어들었다.
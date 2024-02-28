## 프로그래머스 120826번 특정 문자 제거하기

풀이 언어 : JavaScript

- 문제 해결과정
    - 반환해야 하는 값 : 문자열 my_string과 문자 letter이 매개변수로 주어집니다. my_string에서 letter를 제거한 문자열을 return하라
    1. 입력받은 배열을 문자별로 분리해 배열로 저장한다.
    2. forEach문을 사용해 배열안의 요소와 letter을 비교해 다르다면 answer에 추가한다.
    3. answer을 반환한다.

풀이 코드 :

```jsx
function solution(my_string, letter) {
    let answer = '', cnt = 0;
    let characters = my_string.split("");
    characters.forEach(character => {
        if(character != letter[cnt]) answer += character;
    })
    return answer;
}
```

- 다른사람의 풀이
    
    ```jsx
    function solution(my_string, letter) {
        return my_string.replaceAll(letter, "");
    }
    ```
    
    이 코드는 내 코드보다 시간복잡도도 작고, “replaceAll()”이라는 함수를 써서 letter을 “”로 변환함으로써 쉽고 빠르게 문제를 해결하였다.
    
- 새로 알게된점
    - replaceAll() 함수
        
        이 함수는 문자열에서 특정 문자를 다른 문자로 바꿔 주는 역할을 한다.
        
        - 사용 예시
        
        ```jsx
        var 전화번호 = "02-123-4567";
        var 가공된_전화번호 = 전화번호.replaceAll('-',"");
        
        가공된_전화번호 => "021234567"
        ```
        
        .

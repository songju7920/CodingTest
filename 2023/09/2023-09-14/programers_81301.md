# Kakao 2021 숫자 문자열과 영단어

생성일: 2023년 9월 14일 오전 10:33

## 프로그래머스 81301번 숫자 문자열과 영단어

- 문제 해결과정
    - 반환해야 하는 값 : 영어로 된 숫자들을 숫자로 바꾸어 반환하라
    1. 객체를 생성한다.
    2. 배열을 만들고 그 안에 영어로 된 숫자들을 차레대로 넣는다
    3. numArr를 순회하며 정규표현식을 제작하고 replaceall을 사용해 대체시킨다.
    4. answer을 숫자형으로 바꾸어 반환한다.

풀이 코드 :

```jsx
const numbers = {
    zero: 0,  five: 5,
    one: 1,   six: 6,
    two: 2,   seven: 7,
    three: 3, eight: 8,
    four: 4,  nine: 9,
}

function solution(s) {
    let numArr = ["zero", "one", "two", "three", "four", 
                  "five", "six", "seven", "eight", "nine"];
    
    numArr.map(num => {
        let regexp = new RegExp(`${num}`, 'g');
        s = s.replaceAll(regexp, numbers[`${num}`]);
        console.log(s);
    });
    
    return Number(s);
}
```

이 문제는 정규표현식에 대한 지식이 필요해 꽤 어려웠다고 느낀 문제였다.

- 새로 알게된점
    - 정규 표현식 생성시 변수값 넣기
        
        정규표현식에 변수값을 넣어 생성할려면 다음과 같은 문법을 따르면 된다.
        
        ```jsx
        let regexp = new RegExp(`${key}`, "options");
        ```
        
        Ex)
        
        ```jsx
        let num = 1
        let regexp = new RegExp(`${num}`, "g");
        console.log(regexp) // /1/g
        ```
        

- 다른사람의 풀이
    
    ```jsx
    function solution(s) {
        let numbers = ["zero", "one", "two", "three", "four", "five", "six", "seven", "eight", "nine"];
        var answer = s;
    
        for(let i=0; i< numbers.length; i++) {
            let arr = answer.split(numbers[i]);
            answer = arr.join(i);
        }
    
        return Number(answer);
    }
    ```
    
    이 사람은 split을 이용해 그 단어를 기점으로 분리한후, 사이사이에 i값을 넣어서 합치는 식으로 코딩하였다. 진짜 예술적으로 풀었다. 나도 언젠간 이런 코드를 짤 수 있도록 분발해야겠다.
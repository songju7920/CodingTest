## 프로그래머스 120851번 숨어있는 숫자의 덧셈
작성언어 : JS

풀이 코드 분석 :

```jsx
function solution(my_string) {
    var answer = 0; //answer 선언
    //my_string의 길이만큼 반복
    for(let i = 0; i < my_string.length; i++) 
        // my_string[i]가 NaN가 아닌가?
        if(isNaN(Number(my_string[i])) == false)
            //그렇다면 my_string[i]를 answer에 더하라
            answer += Number(my_string[i]);
    return answer; //answer 반환
}
```

처음에는 밑의 코드로 풀기를 시도했었다. 하지만 입력값에 포함되어있는 숫자는 문자열로 취급되기 때문에 (Ex : “D1D2D4”) 0이 출력되는 문제가 있었다.

```jsx
function solution(my_string) {
    var answer = 0;
    for(let i = 0; i < my_string.length; i++)
        if(typeof my_string[i] == "Number")
            answer += my_string[i];
    return answer;
}
```

- 알게된점
    
    isNaN이라는 코드를 오늘 처음 알게되었다. isNaN은 is Not a Number의 약자로, 뒤에 위치한 어떤 값이 NaN인지 판별할때 쓴다. 
    
    예제 코드 :
    
    ```jsx
    isNaN(123) => false //123은 숫자기 때문에 false가 출력된다.
    isNaN("0920") => false //문자열이지만 숫자로 취급하여 false가 출력된다.
    isNaN("") => false //빈 문자열은 0으로 취급한다.
    isNaN("123ABC") => true //문자가 포함되있어 NaN로 취급한다.
    ```

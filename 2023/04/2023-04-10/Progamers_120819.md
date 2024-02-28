## 프로그래머스 120819번 아이스 아메리카노

- 문제 해결 순서
    - return(출력해야 하는 값)
        
        머쓱이가 가지고 있는 돈이 매개변수로 주어질 때, 머쓱이가 최대로 마실 수 있는 아메리카노의 잔 수와 남는 돈을 순서대로 담은 배열을 반환
        
    1. 머쓱이가 가진돈/5500계산해서 answer[0]에 저장
    2. 머쓱이가 가진돈%5500계산해서 answer[1]에 저장
    3. answer return시키기

풀이 코드 :

```jsx
function solution(money) {
    var answer = [];
    answer[0] = ~~(money / 5500);
    answer[1] = money % 5500;
    return answer;
}
```

다른사람의 코드 :

```jsx
function solution(money) {
    return [Math.floor(money / 5500), money % 5500];
}
```
위 코드는 나와 다르게 바로 값을 리턴시켜 코드의 길이를 크게 줄였다.

- 새로 알게된것
    
    Math.floor() : 함수는 주어진 숫자와 같거나 작은 정수 중에서 가장 큰 수를 반환하는 함수 이다.
    
    ```jsx
    Math.floor( 45.95); //  45
    Math.floor( 45.05); //  45
    Math.floor(  4   ); //   4
    Math.floor(-45.05); // -46
    Math.floor(-45.95); // -46
    ```

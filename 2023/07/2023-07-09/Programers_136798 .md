## 프로그래머스 136798 기사단원의 무기

- 문제 해결과정
    - 반환해야 하는 값 : 주어진 숫자와 그 숫자보다 작은 모든 숫자의 약수의 수를 모두 더하되, 약수의 수가 주어진 제한을 넘기면 그 숫자의 약수의 수는 정해진 수로 바꿔 계산.
    1. number의 값을 하나씩 줄여가면서 0보다 클동안 다음 과정 반복
        1. number의 제곱근만큼 아래 반복
            1. number % i가 성립한다면 Cnt값 1증가 하며, 
            number % i가 i와 똑같지 않을경우 1을 추가로 증가
            2. 만약 Cnt가 limit을 넘어갔을경우 Cnt를 limit으로 설정
            3. powers배열에 Cnt를 push
    2. powers배열을 모두 더해서 리

풀이 코드 :

```jsx
function solution(number, limit, power) {
    let powers = [];
    
    while(number != 0){
        let cnt = 0;
        for(let i = 1; i <= Math.pow(number ,0.5); i++){
            if(number % i == 0){
                cnt++;
			          if (i != number / i) cnt++;
            }
        }
        
        //제한넘으면 지정 공격력으로 바꾸기
        if(cnt > limit) cnt = power;
        powers.push(cnt);
        number--;
    }
    
    console.log(powers);
    let answer = powers.reduce((a, b) => a + b)
    return answer;
}
```

이 문제는 시간복잡도에서 크게 애를 먹었던 문제였다. 약수 구하는 알고리즘을 많이 고민하고서야 풀수 있었던 문제였다.

- 효율적 약수 알고리즘
    
    ```jsx
    for(let i = 1; i <= Math.pow(number ,0.5); i++){
                if(number % i == 0){
                    cnt++;
    			          if (i != number / i) cnt++;
                }
            }
    ```
    
    이알고리즘은 주어진 수의 제곱근의 크기만큼만 반복하여 약수를 추출하는 알고리즘이다. 즉, 100이 주어지면 단 10번의 루프만으로 계산이 가능한것이다.
    원리는 다음과 같다.
    16이라는 수가 주어졌을때, 제곱근은 4이므로 구해지는 약수는 1, 2, 4이다.
    이때, 16의 제곱근인 4를 제외하고 나머지 약수인 1,2로 주어진 수를 나누면
    16/1 = 16, 16/2 = 8 이런식으로 추가적인 약수가 나오게 된다.

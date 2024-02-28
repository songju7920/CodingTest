## **프로그래머스 120808번 분수의 덧샘**
풀이 언어 : JS

풀이 코드 분석 :

```jsx
function solution(numer1, denom1, numer2, denom2) {
let topNum = numer1 * denom2 + numer2 * denom1; //분자 계산
let bottomNum = denom1 * denom2; //분모 계산
let max = 1; //max(최대공약수) 선언 및 초기화
//bottomNum보다 작거나 같을동안 반복
for(let i = 1; i <= bottomNum; i++)
{
    //topNum / i가 나누어 떨어지고 bottomNum / i가 나누어 떨어지면
    if(topNum % i == 0 && bottomNum % i == 0) 
    max = i; //max에 i의 값 할당
}
return [topNum/max, bottomNum/max]; //[topNum/max, bottomNum/max] 리턴
}
```

이 문제는 로직을 어떻게 상황에 맞게 출력할지 생각할때 많이 어려웠던 문제이다. 특히, 최대공약수를 구해 나눈다는 생각은 해냈지만 그걸 구현하는데에 많은 어려움이 있었다.

다른사람의 코드 :

```jsx
function fnGCD(a, b){
    return (a%b)? fnGCD(b, a%b) : b;
}

function solution(denum1, num1, denum2, num2) {
    let denum = denum1*num2 + denum2*num1;
    let num = num1 * num2;
    let gcd = fnGCD(denum, num); //최대공약수

    return [denum/gcd, num/gcd];
}
```

위 코드는 함수를 따로 생성하여 코드의 가독성을 높이고 더 알아볼수 쉽게 구현하였다. 또한 재귀함수를 이용하여 반복문을 쓰지 않고 구현하였다.

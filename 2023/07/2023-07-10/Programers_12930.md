## 프로그래머스 12930 **이상한 문자 만들기**

- 문제 해결과정
    - 반환해야 하는 값 : 주어진 문자의 단어마다 짝수번째 알파벳은 대문자, 홀수번째 알파벳은 소문자로 만들어 return.
    1. 문장를 분리
    2. 문장을 forEach문으로 순회
    3. 공백이라면 공백을 result에 넣고 idx값 초기화
        1. 짝수번째라면 대문자로 바꾼 값을 result에 넣고 idx++;
        2. 홀수번째라면 소문자로 바꾼 값을 result에 넣고 idx++;
    4. 배열을 합쳐 리턴

풀이 코드 :

```jsx
function solution(s) {
    let result = [];
    let idx = 0;
    s = s.split("");
    
    s.forEach((char) => {
        if(char == " "){
            result.push(" ");
            idx = 0;
            return 0;
        }else if(!(idx % 2)){
            result.push(char.toUpperCase());
        }else{
            result.push(char.toLowerCase());
        }
        idx++;
    })
    
    return result.reduce((a, b) => a + b);
}
```

이 문제는 로직이 꽤 어려웠던 문제였지만, 함수들만 잘 알고있다면 쉽게 풀 수 있었다.

- 다른 사람의 풀이
    
    ```jsx
    function toWeirdCase(s){
      return s.toUpperCase().replace(/(\w)(\w)/g, function(a){return a[0].toUpperCase()+a[1].toLowerCase();})
    }
    ```
    
    이 사람은 정규 표현식과 replace함수를 사용하여 간단하게 풀었다. 기본적으로 가독성이 내 코드보다 간단하여 유지보수는 간단하겠다는 생각이 들었다.

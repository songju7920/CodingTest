## 프로그래머스 190924 다음에 올 숫자

- 반환해야 하는값
    
    등차수열 혹은 등비수열이 매개변수로 주어질 때, 마지막 원소 다음으로 올 숫자를 return 하도록 solution 함수를 완성해보세요.
    
- 문제 해결과정
    1. 등차수열인지 등비수열인지 확인
    2. 등차수열이라면 등차를 구하여 마지막 요소에 더하기
    3. 등비수열이라면 등비를 구하여 마지막 요소에 곱하기

풀이코드:

```jsx
function solution(common) {
    var answer = 0;
    if(common[1] - common[0] == common[2] - common[1])
        return common[common.length - 1] + common[1] - common[0];
    else
        return common[common.length - 1] * (common[1] / common[0])
}
```

이문제는 배열의 기본개념만 알고 등차수열과 등비수열의 개념만 파악한다면 쉽게 풀수 있다.

- 다른사람의 풀이
    
    ```jsx
    function solution(common) {
        if ((common[1]-common[0])==(common[2]-common[1])){
            return common.pop() + common[1] - common[0];
        }
        else{
            return common.pop()*common[1]/common[0];
        }
    }
    ```
    
    이분은 나의 코드처럼 맨 뒤 요소에 접근하는것 대신 stack자료형의 pop을 사용하여 손쉽게 문제를 해결하였다.
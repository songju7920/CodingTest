## 프로그래머스 120811번 중앙값 구하기

풀이 언어 : JavaScript

- 문제 해결과정
    - 반환해야 하는 값 : 문자열 my_string이 매개변수로 주어질 때 모음을 제거한 문자열을 return하라
    1. array를 sort 함수를 이용하여 배열의 순서를 바쑨다.
    2. Math.floor을 이용하여 소수점 자리를 버린 arr의 index를 반환한다 

풀이 코드 :

```jsx
function solution(array) {
    array.sort(function(a, b){
        if(a > b) return 1;
        if(a == b) return 0;
        if(a < b) return -1;
    });
    return array[Math.floor(array.length/2)];
}
```

- 새로 알게된점
    - sort()함수
        
        배열을 정렬하기 위해서 사용하는 함수
        
        괄호 안의 값이 생략되면, 배열의 element들은 문자열로 취급되어, 유니코드 값 순서대로 정렬됩니다.
        
        - 이 함수가 a, b 두개의 element를 파라미터로 입력받을 경우,
            
            이 함수가 리턴하는 값이 0보다 작을 경우,  a가 b보다 앞에 오도록 정렬하고,
            
            이 함수가 리턴하는 값이 0보다 클 경우, b가 a보다 앞에 오도록 정렬합니다.
            
            만약 0을 리턴하면, a와 b의 순서를 변경하지 않습니다.
            
        
        ```tsx
        const arr = [2, 1, 3, 10];
        
        arr.sort(function(a, b)  {
          if(a > b) return 1;
          if(a === b) return 0;
          if(a < b) return -1;
        });
        document.writeln(arr + '<br>'); // [1, 2, 3, 10]
        ```

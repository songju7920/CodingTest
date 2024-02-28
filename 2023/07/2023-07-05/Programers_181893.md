## 프로그래머스 181893번 배열 조각하기

- 문제 해결 과정
    1. query배열 순회중 다음 과정 수행
        1. 배열의 요소의 인덱스가 짝수라면 [elment + 1]번 인덱스부터 [arr.length-element-1]개의 요소 삭제
        2. 배열의 요소의 인덱스가 홀수라면 0번 인덱스부터 [element]개의 요소 삭제

풀이 코드 :

```jsx
function solution(arr, query) {
    query.forEach((element, idx) => {
        if(idx % 2 == 0) arr.splice(element + 1, arr.length-element-1);
        else arr.splice(0, element);
    })
    
    return arr;
}
```

이번 문제는 splice와 forEach를 사용하여 쉽게 풀수 있었다.

- 새로 알게된점
    - splice VS slice
        
        다른사람의 풀이중 slice를 이용한 풀이도 있어 과연 무엇이 다른지 문득 궁금해져 구글링 해본결과 다음과 같은 차이점이 있었다
        
        slice는 주어진 배열을 변경시키지 않고 값을 추출해 다른곳에 할당해주는 역할을 한다.
        
        반면 splice는 주어진 배열을 변경시키며, 값을 추출해 다른곳에 할당해주는것은 동일했다.
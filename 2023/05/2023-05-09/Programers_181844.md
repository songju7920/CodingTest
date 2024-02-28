## 프로그래머스 181844번 배열의 원소 삭제

풀이 언어 : JavaScript

- 문제 해결과정
    - 반환해야 하는 값 : delete_list의 원소를 모두 삭제하고 남은 원소들은 기존의 arr에 있던 순서를 유지한 배열을 return 하는 solution 함수를 작성해 주세요.
    1. arr에 있는 요소들을 하나씩 delete_list에 있는 요소들과 비교한다
    2. 만약 같지 않다면 Cnt를 1올린다.
    3. 만약 .delete_list.length의 값과 Cnt가 같다면 answer에 element를 추가한다.
    4. answer을 출력한다.

풀이 코드 :

```jsx
function solution(arr, delete_list) {
    var answer = [];
    let location = 0;
    arr.forEach(element => {
        let Cnt = 0;
        for(let i = 0; i < delete_list.length; i++){
            if(element != delete_list[i]){
                Cnt++;
            }
        }
        if(Cnt > delete_list.length-1){
            answer[location] = element;
            location++;
        }
    })
    return answer;
}
```

이번문제는 차근차근 로직을 세우고 화살표 함수를 이용해 forEach문을 사용해 요소들을 하나씩 비교하면 쉽게 풀수 있었다.

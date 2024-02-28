## 프로그래머스 120868 **삼각형의 완성조건(2)**

- 문제 해결과정
    - 반환해야 하는 값 : 삼각형의 두 변의 길이가 담긴 배열 sides가 매개변수로 주어질때, 나머지 한 변이 될 수 있는 정수의 개수를 return.
    1. 삼항 연산자를 사용하여 주어진 길이의 최소, 최대를 구한다
    2. 최소+최대의 크기만큼 반복t
        1. 삼각형 길이 성립공식을 사용
    3. cnt return

풀이 코드 :

```jsx
function solution(sides) {
    let cnt = 0;
    let bigger = sides[0] > sides[1] ? sides[0] : sides[1];
    let smaller = sides[0] < sides[1] ? sides[0] : sides[1];
    
    for(let i = 1; i <= bigger + smaller; i++){
        if((i <= bigger) && (i + smaller > bigger)) cnt++;
        else if((i > bigger) && (bigger + smaller > i)) cnt++;
    }
    return cnt;
}
```

조금만 생각하면 쉽게 풀 수 있는 문제였다.

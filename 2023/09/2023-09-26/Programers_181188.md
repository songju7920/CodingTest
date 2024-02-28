## 프로그래머스 181188번 요격 시스템

- 문제 해결 과정
    1. 미사일들 요격 최소 위치 순으로 정렬
    2. 요격 위치를 지정후 요격 위치에 들어오는 미사일들은 다 요격 판정으로 돌리기
    3. 만약 요격이 불가능한 요격 범위면 요격 위치를 하나 추가한다
    4. 요격 미사일 수를 출력한다

풀이코드 :

```jsx
function solution(targets) {
    targets = targets.sort((a, b) => b[0] - a[0]);
    let points = targets.map(a => a[0]);
    let CurrentPoint = points[0] + 0.1;
    let answer = 1;
    
    for(let i = 1; i < targets.length; i++) {
        if(!(targets[i][0] < CurrentPoint && targets[i][1] > CurrentPoint)) {
            CurrentPoint = points[i] + 0.1;
            answer++;
        }
    }
    
    return answer;
}
```

이 문제는 요격 시스탬을 한번에 어떻게하면 최대로 격추시킬지 고안해내기만 하면 쉬운 문제였다
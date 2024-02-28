## 프로그래머스 42862번 체육복

- 문제 해결과정
    - 반환해야 하는 값 : 체육시간에 출석 가능한 학생의 수를 Return.
    1. 도난당한 학생이 여분이 있는경우 자신의 체육복을 입는다
    2. 자신의 앞뒤 학생이 도난당했을경우 체육복을 빌려준

풀이 코드 :

```jsx
function solution(n, losts, reserve) {
    let canAttend = n - losts.length;
    let length = losts.length;
    reserve.sort((a, b) => b - a)
    losts.sort((a, b) => a - b)
    
    //도난당한 학생이 여분이 있는 경우
    for(let i = 0; i < length; i++) {
        let lost = losts.shift();
        if(reserve.indexOf(lost) != -1) {
            reserve.splice(reserve.indexOf(lost), 1);
            canAttend++;
        } 
        else losts.push(lost);
    }
    
    //빌려주기
    while(losts.length > 0) {
        if(reserve.length < 1) break;
        let size = reserve.pop();
        for(let lost of losts) {
            if(Math.abs(lost - size) == 1){
                losts.splice(losts.indexOf(lost), 1);
                canAttend++;
            }
        }
    }
    
    return canAttend;
}
```

이 문제는 오래전부터 고민하던 문제였는데 생각보다 로직이 간단한 문제였다.

- 다른사람의 풀이
    
    ```jsx
    function solution(n, lost, reserve) {
        const students = {};
        let answer = 0;
        for(let i = 1; i <= n; i++){
            students[i] = 1;
        }
        lost.forEach(number => students[number] -= 1);
        reserve.forEach(number => students[number] += 1);
    
        for(let i = 1; i <= n; i++){
            if(students[i] === 2 && students[i-1] === 0){
                    students[i-1]++;
                    students[i]--;
            } else if(students[i] === 2 && students[i+1] === 0){
                    students[i+1]++;
                    students[i]--;
            }
        }
        for(let key in students){
            if(students[key] >= 1){
                answer++;
            }
        }
        return answer;
    }
    ```
    
    이 코드는 가독성이 정말 좋다. 다른 풀이 코드처럼 난잡하지도, 너무 줄여서 파악이 힘들지도 않고 코딩을 많이 안 접해본 사람들도 문법만 안다면 쉽게 이해할수 있을정도로 코드가 깔끔하다.
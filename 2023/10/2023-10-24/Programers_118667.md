## 프로그래머스 118667번 두 큐 합 같게 만들기

- 문제 해결과정
    - 반환해야 하는 값 : 큐를 몇번 이동시켜야 두 큐의 합을 같게 만들 수 있는지 구하라
    1. 반복 가능 횟수를 구한다(완전탐색 기반)
    2. JS에서 제공한 큐를 그대로 사용하면 시간 복잡도에 걸리기 때문에 시작점을 정해준다.
    3. 둘이 다를때까지 아래 과정을 반복한다.
        1. sum1이 더 크면 queue1에서 dequeue, queue2에 enqueue시킨다.
        2. sum2이 더 크면 queue2에서 dequeue, queue1에 enqueue시킨다.
        3. 반복횟수가 한계치를 넘어간 상태라면 즉시 -1를 리턴하고 함수를 종료한다.
        4. answer를 1증가시킨다.
    4. answer를 return한다.

풀이 코드 :

```jsx
function solution(queue1, queue2) {
    let answer = 0;
    let sum1 = queue1.reduce((a, b) => a + b);
    let sum2 = queue2.reduce((a, b) => a + b);
    let max = queue1.length * 2 + 2;
    let start1 = 0;
    let start2 = 0;
    
    while(sum1 !== sum2) {
        if(sum1 > sum2) {
            let num = queue1[start1];
            queue2.push(num);
            sum1 -= num;
            sum2 += num;
            start1++;
        } else {
            let num = queue2[start2];
            queue1.push(num);
            sum2 -= num;
            sum1 += num;
            start2++;
        }
        
        if(answer > max) return -1;
        answer++;
    }
    
    return answer;
}
```

이 예외처리(아무리 이동 시켜도 두큐의 합이 안같아지는 경우)만 잘 하면 쉬운 문제 였다.

- 다른사람의 풀이
    
    ```jsx
    function solution(queue1, queue2) {
        let answer = 0
        const max = queue1.length*2
        let value = queue1.reduce((acc,cur,idx)=>acc+cur-queue2[idx],0)/2
        let [i,j] = [0,0]
    
        while(value !== 0 && answer < max*2){
            if(value > 0){
                const v = queue1[i]
                i++
                value -= v
                queue2.push(v)
            }else{
                const v = queue2[j]
                j++
                value += v
                queue1.push(v)
            }
            answer++
        }
    
        return value !== 0 ? -1 : answer
    }
    ```
    
    이 코드는 가독성은 약간 떨어지지만 나보다 메모리를 덜 사용하는 코드로 제작되었다.
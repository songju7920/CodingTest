## 프로그래머스 92341번 주차요금 계산

### 문제 해결과정

- 문제 분류 : 구현, 완전탐색
- 반환해야 하는 값 : 주차요금을 계산하여 차량 번호가 작은 순으로 정렬하기
- 풀이과정
    1. Set을 사용하여 차량번호를 중복되지 않게 추출, 정렬하기
    2. totalTime 차량 수만큼 생성 
    3. 입출차 처리
        1. 입차시 시간과 차량번호 기록
        2. 출차시 있던 시간 기록후 totalTime에 기록
    4. 남아있는 차량 처리
    5. 요금 계산하기

### 풀이 코드

```jsx
const calculateTime = (time1, time2) => {
    let [hour1, min1] = time1.split(':').map(a => Number(a));
    let [hour2, min2] = time2.split(':').map(a => Number(a));
    time1 = hour1 * 60 + min1;
    time2 = hour2 * 60 + min2;
    return time2 - time1;
}

function solution(fees, records) {
    let answer = [];
    let parkingLot = [];
    let enterTimes = [];
    let carNums = [...new Set(records.map(r => r.split(' ')[1]))].sort((a, b) => a - b);
    let totalTime =  new Array(carNums.length).fill(0);
    
    // 입출차 처리
    for(let record of records) {
        let [time, number, action] = record.split(' ');
        if(action === 'IN') {
            parkingLot.push(number);
            enterTimes.push(time);
        } else {
            let idx = parkingLot.indexOf(number);
            let enterTime = enterTimes[idx];
            parkingLot.splice(idx, 1);
            enterTimes.splice(idx, 1);
            totalTime[carNums.indexOf(number)] += calculateTime(enterTime, time);
        }
    }
    
    // 남아있는 차량 처리
    while(parkingLot.length > 0) {
        let idx = carNums.indexOf(parkingLot.pop());
        totalTime[idx] += calculateTime(enterTimes.pop(), "23:59");
    }
    
    // 요금 계산
    let [basicTime, basicFee, min ,feePerMin] = fees;
    for(let time of totalTime) {
        if(basicTime <= time) answer.push(basicFee + Math.ceil((time - basicTime) / min) * feePerMin);
        else answer.push(basicFee);
        
    }
    
    return answer;
}
```

코드 시간복잡도 (빅오) : O(n^2)

한줄 회고 : 이 문제는 차량이 주차장에 머무는 시간을 구하는 것과 구한 답들을 차량 번호순으로 배열하는것이 중점인 문제였다.

### 다른사람의 풀이

```jsx
function solution(fees, records) {
    const parkingTime = {};
    records.forEach(r => {
        let [time, id, type] = r.split(' ');
        let [h, m] = time.split(':');
        time = (h * 1) * 60 + (m * 1);
        if (!parkingTime[id]) parkingTime[id] = 0;
        if (type === 'IN') parkingTime[id] += (1439 - time);
        if (type === 'OUT') parkingTime[id] -= (1439 - time);
    });
    const answer = [];
    for (let [car, time] of Object.entries(parkingTime)) {
        if (time <= fees[0]) time = fees[1];
        else time = Math.ceil((time - fees[0]) / fees[2]) * fees[3] + fees[1]
        answer.push([car, time]);
    }
    return answer.sort((a, b) => a[0] - b[0]).map(v => v[1]);
}
```

이 사람은 첫번째 반복문에서 객체를 사용하여 차량의 총 머문 시간을 구하고 두번째 반복문에서 요금을 계산하는 식으로 진행되었다.

내 코드와 제일 다른점은 바로 첫번째 총 머문 시간을 구하는 식에서 하루를 분으로 나눈 값에 1을 뺀 1439에 계산한 시간을 빼고 들어올땐 빼고, 나갈땐 더하는 방식으로 한번에 남아있는 차량의 처리도 해버린 것인데, 이러면 내 코드보다 반복문을 줄일 수 있어 인상 깊었다.

앞으로 이렇게 반복문을 덜 짜는 쪽으로 코딩할 수 있는 로직을 짤 수 있게 노력해야 겠다.

### 새로 알게된점

- 객체에 key-value값이 있는지 없는지 판별하는 방법
    
    단순하게 값을 조회한뒤 if문에 넣으면 처리가 가능하다.
    
    ```jsx
    let object = {apple : 5}
    
    if(!object[banana]) object[banana] = 3;
    if(!object[apple]) object[apple] = 10;
    
    console.log(object) //{ apple : 5, banana: 3 }
    ```
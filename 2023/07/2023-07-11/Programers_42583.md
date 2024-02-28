## 프로그래머스 42583번 **다리를 지나는 트럭**

- 문제 해결 과정
    - 반환해야 하는값 : 트럭이 다 지나는데 걸린 시간
    1. 1일차가 아니고, 다리 위에 트럭이 없을때까지 반복
        1. 만약 먼저 들어온 차량이 나갈 시간이 됬다면 내보니고 총 무게에서 빼주기
        2. 만약 다음 트럭이 들어가도 무게 제한을 넘기지 않는다면 다음 트럭 들여보내기
        3. 시간 넘기기

풀이 코드 :

```jsx
function solution(bridge_length, max_weight, truck_weights) {
    let onTheBridge = [];
    let exitBridgeTime = [];
    let weightSum = 0;
    let time = 1;
    truck_weights.reverse();
    
    while(onTheBridge.length > 0 || time == 1){
        //기존 트럭 처리
        if(exitBridgeTime[0] == time){
            weightSum -= onTheBridge.shift();
            exitBridgeTime.shift();
        }
        
        //새로운 트럭 처리
        let nextTruck = truck_weights.pop();
        
        if(weightSum + nextTruck <= max_weight){
            onTheBridge.push(nextTruck);
            weightSum += nextTruck;
            exitBridgeTime.push(bridge_length + time);
        } else {
            truck_weights.push(nextTruck);
        }
        
        time++;
    }
    
    return time - 1;
}
```

이 문제는 stack과 queue 자료구조의 활용 능력을 테스트하는 문제인 것 같다. 로직 자체는 그닥 그렇게 어렵지 않지만 자료구조로 인해서 LV.2에 위치하고 있는 문제인 것 같다.

- 다른사람의 풀이
    
    ```jsx
    function solution(bridge_length, weight, truck_weights) {
      // '다리'를 모방한 큐에 간단한 배열로 정리 : [트럭무게, 얘가 나갈 시간].
      let time = 0, qu = [[0, 0]], weightOnBridge = 0;
    
      // 대기 트럭, 다리를 건너는 트럭이 모두 0일 때 까지 다음 루프 반복
      while (qu.length > 0 || truck_weights.length > 0) {
        // 1. 현재 시간이, 큐 맨 앞의 차의 '나갈 시간'과 같다면 내보내주고,
        //    다리 위 트럭 무게 합에서 빼준다.
        if (qu[0][1] === time) weightOnBridge -= qu.shift()[0];
    
        if (weightOnBridge + truck_weights[0] <= weight) {
          // 2. 다리 위 트럭 무게 합 + 대기중인 트럭의 첫 무게가 감당 무게 이하면 
          //    다리 위 트럭 무게 업데이트, 큐 뒤에 [트럭무게, 이 트럭이 나갈 시간] 추가.
          weightOnBridge += truck_weights[0];
          qu.push([truck_weights.shift(), time + bridge_length]);
        } else {
          // 3. 다음 트럭이 못올라오는 상황이면 얼른 큐의
          //    첫번째 트럭이 빠지도록 그 시간으로 점프한다.
          //    참고: if 밖에서 1 더하기 때문에 -1 해줌
          if (qu[0]) time = qu[0][1] - 1;
        }
        // 시간 업데이트 해준다.
        time++;
      }
      return time;
    }
    ```
    
    이 사람은 만약 트럭이 더 올라갈 수 없는 상태라면 첫 번째 트럭이 나가는 시점으로 시간을 점프하면서 시간복잡도를 상대적으로 엄청나게 줄여 효율성을 엄청나게 올렸다. 또한 다른 개발자들과 소통을 잘 할 수 있도록 주석을 꼼꼼히 달아놓은 모습도 정말 존경스러웠다. 언젠가는 나도 아런 개발자가 될 수 있으면 좋겠다.

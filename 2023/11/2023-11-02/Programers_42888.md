## 프로그래머스 42888번 오픈채팅방

### 문제 해결과정

- 문제 분류 : 해시, 구현
- 반환해야 하는 값 : 오픈채팅방의 출입기록
- 주의 사항
    - 같은 userID를 가진 사용자가 닉네임을 바꾸면 전에 있던 해당 사용자에 대한 출입기록의 닉네임도 바꾸어야 한다.
- 풀이과정
    1. 해시 알고리즘을 사용하여 유저아이디마다 고유한 닉네임을 가지게 설정
    2. 만약 닉네임이 바뀔시 해당 해시를 업데이트
    3. 해시테이블을 바탕으로 출입기록 구성후 배열에 담기

### 풀이 코드

```jsx
function solution(records) {
    let hashTable = new Map();
    let result = [];

    // 최종 닉네임 도출
    records.map(record => {
        let [action, userID, nickname] = record.split(' ');

        if(!hashTable.has(userID)) {
            hashTable.set(userID, nickname);
        } else {
            if(action == 'Change') {
                hashTable.set(userID, nickname);
            } else if(action == 'Enter' && hashTable.get(userID) != nickname) {
                hashTable.set(userID, nickname);
            }
        }
    })

    // 메세지 생성
    records.map((record, idx) => {
        let [action, userID, nickname] = record.split(' ');
        nickname = hashTable.get(userID);
        if(action == "Enter") {
            result.push(`${nickname}님이 들어왔습니다.`);
        } else if (action == "Leave") {
            result.push(`${nickname}님이 나갔습니다.`);
        }
    })

    return result;
}
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 이 문제를 어떻게 풀지 고민하고있을때 아침에 공부했던 해시가 뇌리에 스쳐갔다. 마침 유저아이디도 고유하니 최적의 알고리즘이라고 생각하였고 로직을 구성했다.

### 다른사람의 풀이

```jsx
function solution(record) {
    const userInfo = {};
    const action = [];
    const stateMapping = {
        'Enter': '님이 들어왔습니다.',
        'Leave': '님이 나갔습니다.'
    }

    record.forEach((v) => {
        const [state, id, nick] = v.split(' ');

        if(state !== "Change") {
            action.push([state, id]);
        }

        if(nick) {
            userInfo[id] = nick;
        }
    })

    return action.map(([state, uid]) => {
        return `${userInfo[uid]}${stateMapping[state]}`;    
    })
}
```

이 코드를 실행해보면 테스트 29가 내 코드는 약 300ms, 이 코드는 약 230ms정도로 이 풀이가 시간복잡도가 훨씬 적었다.

그래서 결정적인 차이점이 대체 무엇일까 고민을 해보니 크게 2가지로 결론이 났다

- 최종 닉네임을 도출할때, 내 코드가 이 코드보다 조건문을 더 많이 사용하였다.
- 최종 답안을 작성할때 내 코드는 조건문이 존재하지만, 이 코드는 조건문이 없는 것을 확인할 수 있다.

특히 stateMapping으로 입출력 문장을 객체로 묶어놓은것이 정말 인상 깊다. 이러면 마지막에 나처럼 조건문을 사용하지 않아도 객체에 접근함으로써 값을 도출해낼 수 있다.
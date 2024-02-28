## 프로그래머스 68645번 **삼각 달팽이**

### 문제 해결과정

- 문제 분류 : 2차원 배열
- 반환해야 하는 값 : 길이와 높이가 n인 삼각형에서 맨 위 꼭짓점부터 반시계 방향으로 달팽이 채우기를 진행한 후, 첫 행부터 마지막 행까지 모두 순서대로 합친 새로운 배열을 반환
- 풀이과정
    1. 삼각형 모양으로 배열을 생성한다.
    2. 반복 횟수를 구한다
    3. moves 배열로 가야하는 방향을 저장해둔다.
    4. 배열에 1부터 반복횟수까지의 수를 정해진 위치에 저장한다.
    5. 배열의 범위를 벗어나거나 0이 아니라면 방향을 바꾼다.
    6. 배열을 합친다

### 풀이 코드

```jsx
function solution(n) {
    var answer = [];
    let repeat = 0;
    for(let i = 1; i <= n; i++) {
        answer.push(new Array(i).fill(0));
        repeat += i;
    }

    let moveLevel = 0;
    let location = [0, 0];
    let moves = [[1, 0], [0, 1], [-1, -1]];
    for(let i = 0; i < repeat; i++) {
        answer[location[0]][location[1]] = i + 1;

        let move = moves[moveLevel % 3];
        try {
            answer[location[0] + move[0]][location[1] + move[1]] == null
            if (answer[location[0] + move[0]][location[1] + move[1]] != 0) moveLevel++;
        } catch (err) {
            moveLevel++;
        }
        move = moves[moveLevel % 3];
        location[0] += move[0];
        location[1] += move[1];
    }

    return answer.reduce((a, b) => [...a, ...b]);
}
```

코드 시간복잡도 (빅오) : O(n) 

한줄 회고 : 이번 코드는 조금 더럽게 짠 코드이다. 개선할 수 있는 방식을 찾는 것이 중요할 것 같다.

### 다른사람의 풀이

```jsx
function solution(n) {
  let a = Array(n).fill().map((_, i) => Array(i + 1).fill())
  let row = -1
  let col = 0
  let fill = 0
  for (let i = n; i > 0; i -= 3) {
    for (let j = 0; j < i; j++) a[++row][col] = ++fill
    for (let j = 0; j < i - 1; j++) a[row][++col] = ++fill
    for (let j = 0; j < i - 2; j++) a[--row][--col] = ++fill
  }
  return a.flat()
}
```

이 코드는 위에서부터 삼각형 배열을 한겹씩 채우는 코드이다 가독성도 매우 좋고 로직도 매우 간단한 아주 좋은 코드이다. 앞으로 이런 문제를 만날때는 이런 로직을 이용하는 것이 좋겠다고 생각했다.

### 새로 알게된점

- array.flat
    
    ```jsx
    let array = [[1], [2, 3, 4], [5, 6, 7, 8], [9]];
    console.log(array.flat()) //[1, 2, 3, 4, 5, 6, 7, 8, 9]
    ```
    
    이 메소드는 2차원 배열을 1차원 배열로 합쳐주는 메소드이다.
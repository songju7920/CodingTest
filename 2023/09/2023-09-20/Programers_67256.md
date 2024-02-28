# Kakao 2020 키패드 누르기

생성일: 2023년 9월 20일 오후 6:44

## 프로그래머스 67256번 키패드 누르기

- 문제 해결과정
    - 반환해야 하는 값 : 키패드를 누르는 손가락 순서를 문자열에 담아서 출력
    1. 2차원 좌표에 대응되는 배열을 선언한다
    2. locationL, locationR을 지정한다.
    3. 왼쪽 3글자(1, 4, 7)은 왼쪽손으로 누르게 처리하고 오른쪽 3글자(3, 6, 9)도 같은 방법으로 처리한다.
    4. 가운데 버튼을 눌러야 한다면 좌표를 가지고 맨하탄 계산법을 사용하여 거리를 구하고 비교해 어떤 손으로 누를지 결정한다.

풀이 코드 :

```jsx
const manhattanDistance = (location1, location2) => {
  let x = Math.abs(location1[0] - location2[0]);
  let y = Math.abs(location1[1] - location2[1]);

  return x+y;
}

function solution(numbers, hand) {
    var answer = '';
    let leftHand = [3, 0], rightHand = [3, 2];
    let keyPad = [[3, 1], [0, 0], [0, 1], [0, 2], [1, 0], [1, 1], [1, 2], [2, 0], [2, 1], [2, 2]];
    numbers.map(number => {
        if(number % 3 == 1){
            leftHand = keyPad[number];
            answer += "L";
        } else if(number % 3 == 0 && number != 0) {
            rightHand = keyPad[number];
            answer += "R";
        } else {
            let disL = manhattanDistance(leftHand, keyPad[number]);
            let disR = manhattanDistance(rightHand, keyPad[number]);
            
            if(disL > disR || disL == disR && hand == 'right') {
                rightHand = keyPad[number];
                answer += "R";
            } else {
                leftHand = keyPad[number];
                answer += "L";
            }
        }
    })
    return answer;
}
```

이 문제는 맨하탄 계산법이라는 계산법을 알고있어야 풀 수 있었던 문제였다. 맨하탄 계산법이 무엇인지는 후술하도록 하겠다.

- 새로 알게된점
    
    맨하탄 계산법
    
    거리를 구할때 사용하는 계산법으로 간단히 x차이의 절대값, y차이의 절대값을 더하면 된다
    
    ```jsx
    |x1-x2| + |y1-y2|
    ```
## 프로그래머스 17687번 N진수 게임

- 문제 해결과정
    - 반환해야 하는 값 : 진수게임에서 진수의 값 N, 시작 순서 P, 구할 개수 T, 사람의 수 M이 주어질때 말해야하는 숫자를 Return
    1. m * t보다 numArr의 길이가 작을때 n진수로 바꾸어 나눈뒤 삽입한다.
    2. 구해야 하는 원소 값들을 뽑아와 Answer에 더한다.
    3. 11진수 이상 처리를 위하여 toUpperCase를 사용한다.

풀이 코드 :

```jsx
function solution(n, t, m, p) {
    let answer = '';
    let numArr = [];
 
    for(let i = 0; m * t > numArr.length; i++) {
        numArr.push(...i.toString(n).split(''));
    }
    
    for(let i = 0; i < t * m; i += m) {
				answer += numArr[p + i - 1];
		}
    
    return answer.toUpperCase();
}
```

이 문제는2진수와 split(분리)처리만 잘 한다면 쉬운 문제였다.

- 다른사람의 풀이
    
    ```jsx
    function solution(n, t, m, p) {
        var tubeT = Array.apply(null,Array(t)).map((a,i)=>i*m+p-1);
        var line = '';
        var max = m*t + p;
        for (var i =0;line.length <= max; i++) {
            line += i.toString(n);
        }
        return tubeT.map(a=>line[a]).join('').toUpperCase();
    }
    ```
    
    이 코드는 가독성은 떨어지지만 코드의 성능은 뛰어난 코드이다.
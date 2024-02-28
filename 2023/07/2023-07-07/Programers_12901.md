# [7/07]

생성일: 2023년 7월 7일 오전 11:22

## 프로그래머스 12901번 **2016년**

- 문제 해결 과정
    
    2016년 a월 b일이 주어질때 무슨 요일인지 return
    
    - return해야 하는값
        1. weekData 배열 생성
        2. 월 수만 큼 반복
            1. 각 달에 맞는 일수 더해주기
        3. 일수 더해주기
        4. weekData[days % 7] return

풀이 코드 :

```jsx
function solution(a, b) {
    var days = 0;
    let weekData = [ "THU", "FRI", "SAT", "SUN", "MON", "TUE", "WED"];
    
    //월 처리
    for(let i = 1; i < a; i++){
        if((i < 8 && i % 2 == 1) || (i > 7 && i % 2 == 0)) {
            days += 31;
        } else if(i == 2) { 
            days += 29;
        } else { 
            days += 30;
        }
    }
    
    days += b;
    
    return weekData[days % 7]
}
```

만만하게 보고 들어온 문제였는데 생각보다 월 처리하는데 어려웠던 문제였다.

- 다른 사람의 풀이
    
    ```jsx
    function getDayName(a,b){
      var dayList = ['FRI','SAT','SUN','MON','TUE','WED','THU'];
      var monthArr = [31, 29, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31];
      var daySum;
      if(a < 2) {
        daySum = b - 1;
      } else {
        daySum = monthArr.slice(0, a - 1).reduce((a, b) => a + b) + b - 1;
      }
        return dayList[daySum % 7];
    }
    
    //아래 코드는 테스트를 위한 코드입니다.
    console.log(getDayName(5,24));
    console.log(getDayName(1,19));
    ```
    
    이 사람의 풀이는 나처럼 반복문과 조건문을 이용한 풀이가 아니고, 각 달의 날 수를 배열에 담아 slice와 reduce를 이용하여 날 수를 계산하였다. 물론 반복문을 사용하지 않았으므로 나보다 시간 복잡도와 가독성이 훌륭한 코드이다
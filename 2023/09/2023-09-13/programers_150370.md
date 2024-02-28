## 프로그래머스 150370번 개인정보 수집 유효기간

- 문제 해결과정
    - 반환해야 하는 값 : 파기해야할 개인정보들의 번호를 배열에 담아 반환하라
    1. term을 dictionary화 시킨다. (이때 value는 Number형으로 바꾸어 저장한다)
    2. privacies배열 순회 시작
        1. privacy를 계약 날자와 조약 번호로 분리한다.
        2. 계약날자에 조약 기간을 불러와 더한다.
        3. 오늘 날짜와 비교한다.
        4. 만약 기한이 지났다면 answer배열에 push시킨다.

풀이 코드 :

```jsx
function solution(today, terms, privacies) {
    var answer = [];
    
    let termObj = {}
    
    terms.map(term => {
        let [termName, termPeriod] = term.split(" ");
        termObj[`${termName}`] = Number(termPeriod);
    })

    privacies.map((privacy, idx) => {
        const [contractDate, term] = privacy.split(" ");
        
        //종료일 계산
        let [Cyear, Cmonth, Cdate] = contractDate.split(".");
        Cyear = Number(Cyear);
        Cmonth = Number(Cmonth);
        Cdate = Number(Cdate);
        
        Cmonth += termObj[term];
        while(Cmonth > 12) {
            Cyear += 1; 
            Cmonth -= 12;
        }
        
        //시간 비교
        let [Tyear, Tmonth, Tdate] = today.split(".");
        Tyear = Number(Tyear);
        Tmonth = Number(Tmonth);
        Tdate = Number(Tdate);
        
        if(Tyear > Cyear) answer.push(idx + 1);
        if (Tyear === Cyear && Tmonth > Cmonth) answer.push(idx + 1);
        if (Tyear === Cyear && Tmonth === Cmonth && Tdate >= Cdate) answer.push(idx + 1);
    })
    
    return answer;
}
```

이 문제는 차근차근 풀고 날짜 계산만 정확히 할 수 있다면 쉽게 풀 수 있었다.

- 새로 알게된점
    
    dictionary
    
    말그대로 사전처럼 저장할 수 있는 자료구조
    
    ```jsx
    let dictionary = {}
    
    dictionary["test"] = 1;
    dictionary["test2"] = "wow";
    console.log(dictionary); // {"test" : 1, "test2" : "wow"}
    delete dictionary["test"];
    console.log(dictionary); // {"test2" : "wow"}
    ```
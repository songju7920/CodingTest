## 프로그래머스 92334번 신고 결과 받기

- 문제 해결과정
  - 반환해야 하는 값 : 신고처리 메일을 보내야하는 횟수를 배열에 담아서 반환
  1. Set을 사용해 중복을 제거한다
  2. reports를 순회하며 신고받은 횟수를 기록한다
  3. 신고 횟수를 기반으로 밴을 먹일 유저들을 검사한다.
  4. reports배열을 한번 더 순회하며 밴먹은 유저들을 신고한 사람들에게 신고 처리 매일을 보내야 하는 횟수를 계산한다.

풀이 코드 :

```jsx
function solution(id_list, reports, k) {
  let answer = new Array(id_list.length).fill(0);
  let reportedCnts = new Array(id_list.length).fill(0);
  let bannedList = [];
  reports = [...new Set(reports)];

  reports.map((report) => {
    let accused = report.split(" ")[1];
    reportedCnts[id_list.indexOf(accused)]++;
  });

  reportedCnts.map((reportedCnt, idx) => {
    if (reportedCnt >= k) bannedList.push(id_list[idx]);
  });

  reports.map((report) => {
    let [reporter, reported] = report.split(" ");
    if (bannedList.indexOf(reported) != -1) {
      answer[id_list.indexOf(reporter)]++;
    }
  });

  return answer;
}
```

이 문제는 처음에 이중 반복문을 사용하여 풀려고 하여 시간복잡도 제한에 걸렸던 문제였다. 그래서 로직을 재설계하여 이중반복문이 없는 로직으로 재구성하여 풀었던 문제였다.

- 다른 사람의풀이
  ```jsx
  function solution(id_list, report, k) {
    let reports = [...new Set(report)].map((a) => {
      return a.split(" ");
    });
    let counts = new Map();
    for (const bad of reports) {
      counts.set(bad[1], counts.get(bad[1]) + 1 || 1);
    }
    let good = new Map();
    for (const report of reports) {
      if (counts.get(report[1]) >= k) {
        good.set(report[0], good.get(report[0]) + 1 || 1);
      }
    }
    let answer = id_list.map((a) => good.get(a) || 0);
    return answer;
  }
  ```
  이사람은 Map자료형을 이용하여 깔끔하게 코드를 작성하였다. 하지만 변수 이름이 good과 bad보단 reporter, reported같은 더 직관적인 이름이였으면 좋았을 것 같다.

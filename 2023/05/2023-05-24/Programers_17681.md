## 프로그래머스 17681번 비밀지도

- 문제 해결과정
  - 반환해야 하는 값 : 비밀지도의 암호를 해독하는 작업을 도와줄 프로그램을 작성하라.
  1. 각 데이터를 가져와서 2진수로 변환시킨다.
  2. n의 값만큼 다음을 반복한다
     1. 2진수 데이터들을 분리시킨다.
     2. 2진수 데이터들을 1과 0으로 판별한다.
  3. 결과를 도출한다.

풀이 코드 :

```jsx
function solution(n, arr1, arr2) {
  let MapData1 = [],
    MapData2 = [];
  let answer = [];

  //2진수 변환
  arr1.forEach((element) => {
    MapData1.push(element.toString(2).padStart(n, "0"));
  });
  arr2.forEach((element) => {
    MapData2.push(element.toString(2).padStart(n, "0"));
  });

  //지도 데이터 합치기
  for (let i = 0; i < n; i++) {
    let Map = "";
    let Data1 = MapData1[i].split("");
    let Data2 = MapData2[i].split("");
    for (let j = 0; j < n; j++) {
      if (Data1[j] == "1" || Data2[j] == "1") Map += "#";
      else Map += " ";
    }
    answer.push(Map);
  }

  return answer;
}
```

이번 문제는 생각외로 쉽게 풀렸는데, 0이 앞에 들어가야 하는 경우가 있어 조금 고전했던 문제였다.

- 새로 알게된점
  padStart/End함수
  문자열의 길이를 맟추고싶을때 쓰는 함수이며, 아래 문법으로 사용할수있다.
  ```jsx
  //앞에 추가
  let newArr1 = Arrayname.padStart(원하는 길이, "넣을 문자");
  //뒤에 추가
  let newArr2 = Arrayname.padEnd(원하는 길이, "넣을 문자");
  ```

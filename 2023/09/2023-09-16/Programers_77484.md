## 프로그래머스 77484번 로또의 최고 순위와 최저 순위

- 문제 해결과정
    - 반환해야 하는 값 : 로또의 번호가 주어질 시 최고순위와 최저순위를 구해라
    1. lottos를 순회하며 로또번호를 추출한다
        1. 만약 로또번호가 0(알수없음)이라면 max를 1추가한다
        2. 만약 로또번호가 0이 아니고 당첨번호에 포함되어 있다면 max와 least를 둘다 1씩올린다.
    2. max나 least에 변화가 존재하지 않았다면 변화가 존재 안한 변수를 1 감소시킨다.

풀이 코드 :

```jsx
function solution(lottos, win_nums) {
    let least = 7, max = 7;
    
    lottos.map(lottoNum => {
        if(lottoNum == 0){
            max--;
        } else if(win_nums.indexOf(lottoNum) != -1) {
            max--;
            least--;
        }
    });
    
    if(max == 7) max--;
    if(least == 7) least--;
    
    return [max, least];
}
```

이 문제는 다른 카카오 문제들보단 매우 쉬웠던 문제였다.

- 다른사람의 풀이
    
    ```jsx
    function solution(lottos, win_nums) {
        const rank = [6, 6, 5, 4, 3, 2, 1];
    
        let minCount = lottos.filter(v => win_nums.includes(v)).length;
        let zeroCount = lottos.filter(v => !v).length;
    
        const maxCount = minCount + zeroCount;
    
        return [rank[maxCount], rank[minCount]];
    }
    ```
    
    이사람은 순위를 배열로 정하고 filter로 min과 zero를 카운트 후 max를 계산하고 배열에 idx로 넣어서 해결하였다. 배열로 순위를 파악한게 정말 인상깊었다.
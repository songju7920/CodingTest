## 프로그래머스 17680번 캐시

- 문제 해결과정
    - 반환해야 하는 값 : 프로그램을 실행할 때 총 실행 시간을 계산하여라.
    1. cacheSize가 0이면 cities 길이에 5를 곱해서 return한다.
    2. cities를 순회하며 다음작업을 수행한다.
        1. city를 소문자로 모두 바꾼다.
        2. city가 캐시에 있는지 확인하고, 있다면 그 캐시를 캐시 제일 상단에 올리고 실행시간을 1초 증가시킨다.
        3. 캐시가 가득 찼는지 확인하고, 가득 찼다면 제일 오래전에 사용된 데이터 하나를 삭제하고 새로운 데이터를 넣는다.
        4. 둘다 해당되지 않는다면 그냥 데이터를 삽입한다.

풀이 코드 :

```jsx
// cache using LRU = queue

function solution(cacheSize, cities) {
    let answer = 0;
    let cache = [];
    
    if(cacheSize == 0){
        return cities.length * 5;
    }
    
    cities.map(city => {
        city = city.toLowerCase();
        let cacheIdx = cache.indexOf(city);
        if(cacheIdx != -1) {
            cache.splice(cacheIdx, 1);
            cache.push(city);
            answer += 1;
        } else if (cache.length == cacheSize) {
            cache.shift();
            cache.push(city);
            answer += 5;
        } else {
            cache.push(city);
            answer += 5;
        }
    })
    
    return answer;
}
```

이 문제는 LRU 캐시가 Queue구조로 돌아간다는 지식을 알고있다면 쉽게 풀 수 있었던 문제였다.

- 다른사람의 풀이
    
    ```jsx
    function solution(cacheSize, cities) {
        if (!cacheSize) return cities.length*5;
    
        const cache = [];
        let time = 0;
        for (const city of cities){
            const city_low = city.toLowerCase();
            if (cache.includes(city_low)) {
                cache.splice(cache.indexOf(city_low), 1);
                cache.push(city_low);
                time++;
                continue;
            }
    
            cache.push(city_low);
            time += 5;
    
            if (cache.length > cacheSize) cache.shift();
        }
    
        return time;   
    }
    ```
    
    이사람은 contenue를 사용하여 코드를 가독성 좋게 깔끔하게 작성하였다.
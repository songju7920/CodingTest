## 백준 25183번 인생은 한 방

- 문제 해결과정
  - 반환해야 하는 값 : 배열의 값중 사전상으로 이웃하는 글자가 5개 이상 연속해 있을경우 YES를, 아닐경우 NO를 출력
  1. 반복횟수 n과 로또 문자열 lottory을 입력 받기
  2. 배열 순회하며 다음 배열의 글자가 사전상으로 이웃해 있다면 cnt++를, 아니라면 cnt를 1로 바꾸기
  3. cnt가 5이상이면 YES를 아니면 NO를 출력

풀이 코드 :

```jsx
#include <stdio.h>
#include <string.h>

int main() {
  int n;
  int cnt = 1;
  scanf("%d", &n);

  char lottory[n + 1];
  scanf("%s", lottory);

  for (int i = 0; i < n - 1; i++) {
    if (lottory[i] + 1 == lottory[i+1]) {
      cnt++;
    } else if (lottory[i] - 1 == lottory[i+1]) {
      cnt++;
    } else {
      cnt = 1;
    }

    //5개 연속시 종료
    if (cnt == 5) {
      break;
    }
  }

  if (cnt >= 5) {
    printf("YES");
  } else {
    printf("NO");
  }
}
```

이 문제는 배열에 대한 이해와 ASCII코드가 뭔지만 알고 있다면 쉽게 풀 수 있었던 문제였다 .

- 다른 사람의 풀이
  ```jsx
  #include <stdio.h>
  #include <stdlib.h>
  #include <string.h>

  int main(){
      int N;
      scanf("%d", &N);
      char* s = malloc(sizeof(char) * (N+1));
      scanf("%s", s);

      int c;
      int count = 1;
      int prev = s[0];
      for (int i = 0; i < N-1; i++){
          c = s[i] - s[i+1];
          if (abs(c) == 1){
              count++;
          }
          else{
              count = 1;
          }
          if (count == 5){
              printf("YES\n");
              return 0;
          }
      }
      printf("NO\n");
      return 0;
  }
  ```
  이 사람은 동적 할당을 통해 메모리의 사용을 최대한 줄이고, abs를 사용해 가독성 있게 코드를 매우 깔끔하게 짰다. 진짜로 너무 깔끔해서 기립박수가 나올 정도로 코드가 깔끔하다.

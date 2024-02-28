## 백준 **16675**번 두개의 손

- 문제 해결과정
  - 반환해야 하는 값 : 민성이와 태경이의 손의 상태가 주어질때 민성이가 무조건 이기는 경우엔 MS, 태경이가 무조건 이기는 경우엔 TK, 알수 없는 경우는 ?를 출력하라.
  1. 태경이가 낸 손의 상태가 같고, 민성이가 태경이를 이길수 있는 손이 있다면, MS를 출력하고 프로그램을 종료하라.
  2. 민성이가 낸 손의 상태가 같고, 태경이가 민성이가 이길수 있는 손이 있다면, TK를 출력하고 프로그램을 종료하라.
  3. 둘다 아니면 ?를 출력한다.

풀이 코드 :

```jsx
#include <stdio.h>

int main(void) {
  char MS[2];
  char TK[2];

  scanf("%c %c %c %c", &MS[0], &MS[1], &TK[0], &TK[1]);

  if (MS[0] == MS[1]) {
    if (MS[0] == 'R' && TK[0] == 'P' || MS[0] == 'R' && TK[1] == 'P') {
      printf("TK");
      return 0;
    }
    if (MS[0] == 'P' && TK[0] == 'S' || MS[0] == 'P' && TK[1] == 'S') {
      printf("TK");
      return 0;
    }
    if (MS[0] == 'S' && TK[0] == 'R' || MS[0] == 'S' && TK[1] == 'R') {
      printf("TK");
      return 0;
    }
  }

  if (TK[0] == TK[1]) {
    if (TK[0] == 'R' && MS[0] == 'P' || TK[0] == 'R' && MS[1] == 'P') {
      printf("MS");
      return 0;
    }
    if (TK[0] == 'P' && MS[0] == 'S' || TK[0] == 'P' && MS[1] == 'S') {
      printf("MS");
      return 0;
    }
    if (TK[0] == 'S' && MS[0] == 'R' || TK[0] == 'S' && MS[1] == 'R') {
      printf("MS");
      return 0;
    }
  }

  printf("?");
}
```

이 문제는 조건문을 하나하나 설정하는게 매우 힘들었던 문제였다.

- 다른사람의 풀이
  ```tsx
  function solution(array, commands) {
    return commands.map((command) => {
      const [sPosition, ePosition, position] = command;
      const newArray = array
        .filter(
          (value, fIndex) => fIndex >= sPosition - 1 && fIndex <= ePosition - 1
        )
        .sort((a, b) => a - b);

      return newArray[position - 1];
    });
  }
  ```
  이 사람은 filter을 사용하여 요소를 뽑아낸뒤 sort를 하여 리턴하는 방식으로 풀었다.

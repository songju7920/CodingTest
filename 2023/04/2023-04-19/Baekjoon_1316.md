## 백준 1316번 그룹 단어 체커

문제 해결 과정

반환해야 하는 값 : 그룹 단어의 개수를 출력한다

1. N에 몇개의 문자열을 입력받을지 입력받는다.
2. N만큼 다음의 내용을 반복한다:
    1. 문자열을 입력받는다.
    2. 문자열의 길이만큼 다음 내용을 반복한다:
        1. 자기 자신과 같고, 연속되지 않는 문자가 있다면 Cnt를 하나 감소시킨다.

풀이 코드 :

```tsx
#include <stdio.h>
#include <string.h>

int main(void) {
  char str[101];
  int N;
  scanf("%d", &N);
  int Cnt = N;

  for (int i = 0; i < N; i++) {
    scanf("%s", str);

    for (int j = 0; j < strlen(str); j++)
      for (int k = j+1; k < strlen(str); k++)
        if(str[j] == str[k] && str[k-1] != str[k]){
          Cnt--;
          goto jump;
        }
    jump:;
  }

  printf("%d", Cnt);
  return 0;
}
```

이번 문제는 로직을 순서대로 설계하고 구현하면 쉽게 구현할수 있었다. 또한 goto문을 처음 사용해봤는데, 원하는위치로 쉽게 이동할수 있다는것이 너무 신기했다.

새로 알게 된점

- goto문
    
    코드의 원하는 부분으로 이동할수 있다. 사용법은 다음과 같다.
    
    ```tsx
    //시작 코드
    goto skip;
    //스킵해도 되는 코드
    skip:
    //코드 종료
    ```

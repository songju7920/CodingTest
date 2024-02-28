## 백준 1157 단어공부

- 문제 해결 과정
    1. 문자열을 입력받는다.
    2. 문자열 맨 끝과 맨앞을 비교한다
    3. 문자열 2번째에 있는 글자와 뒤에서 2번쨰에 있는 글자를 비교한다.
    4. 이과정을 반복한다

풀이 코드 :

```tsx
#include <stdio.h>
#include <string.h>

int main(void) {
  char str[100];
  int result = 1;
  scanf("%s",str);

  size_t str_len = strlen(str);
  for(int i = 0; i < str_len; i++) {
    if(str[str_len - 1 - i] != str[i]) {
      result = 0;
      break;
    }
  }
  printf("%d",result);
}
```

이번 문제는 문자열 배열과 반복문을 사용하면 쉽게 풀수 있었다

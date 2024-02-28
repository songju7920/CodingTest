## 백준 1152번 단어의 개수

풀이 코드 :

```c
#include <stdio.h>
#include <string.h>

int main (void)
{
  char String[1000000];
  int Cnt = 0;
  
  scanf("%[^\n]", String);

  for(int i = 1; i < strlen(String); i++)
      if(String[i] == ' ' && i != strlen(String) - 1)
        Cnt++;
  if(strlen(String) == 1 && String[0] == ' ')
    printf("0");
  else
    printf("%d", Cnt + 1);
}
```

이번 문제는 단어가 공백 하나만 입력될 반례를 생각하지 못해 꽤 힘들었다. 앞으로 이런 문제들을 계속 풀어보며 반례를 쉽게 알아낼수 있는 사고력을 키워야겠다고 생각했다.

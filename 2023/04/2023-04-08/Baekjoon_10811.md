## 백준 10809번 알파벳 찾기

풀이 코드 :

```c
#include <stdio.h>
#include <string.h>

int main (void)
{
  char String[100];
  int location[100];
  
  for(int i = 0; i < 100; i++)
    location[i] = -1;
  
  scanf("%s", String);
  for(int a = 97; a < 123; a++)
    for(int i = 0; i < strlen(String); i++)
      if (String[i] == (char)a)
      {
        location[a - 97] = i;
        break;
      }
  
  for(int i = 0; i < 26; i++)
    printf("%d ",location[i]);
}
```

문자열이 배열이라는것을 알고있고, 제어문 반복문을 적절히 쓸수 있으면 쉽게 해결할수 있는 문제였다.

## 백준 2839번 설탕 배달

풀이 코드 :

```c
#include <stdio.h>

int main (void)
{
  int Num, sugarBag = 0;
  scanf("%d", &Num);
  
  while(Num > 0) {
      if(Num >= 3 && Num % 5 != 0) {
          sugarBag++;
          Num -= 3;
          continue;
        }
      else if (Num >= 5) {
          sugarBag++;
          Num -= 5;
          continue;
      }
      else
        break;
    }
  
  if(Num == 0)
    printf("%d" , sugarBag);
  else 
    printf("-1"); 
}
```

이 문제는 내가 푼 첫 실버 문제였다. 이 문제는 처음 코드 설개는 어렵지만 조금만 생각하면 풀수 있을정도의 난이도였다.

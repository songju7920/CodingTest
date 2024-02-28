## 백준 1546번 평균
풀이 언어 : C

풀이 코드 :

```c
#include <stdio.h>

int main (void)
{
  int subjectCnt, max = 0;
  double result;
  scanf("%d", &subjectCnt);
  int score[subjectCnt];
  for(int i = 0; i < subjectCnt; i++) {
      scanf("%d", &score[i]);
      if(score[i] > max)
        max = score[i];
    }
  for(int i = 0; i < subjectCnt; i++) {
      result += (double)score[i] / max * 100;
    }
  printf("%lf",result/subjectCnt);
}
```

이번 문제는 코드를 짜는것보다 문제를 이해하는게 더 힘든 문제였다. 문제를 더 세분화하고 단계별로 구축 하는 연습을 더 해야겠다.

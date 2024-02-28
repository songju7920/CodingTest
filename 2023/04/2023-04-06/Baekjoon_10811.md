## 백준 10811번 바구니 뒤집기

풀이코드 :

```c
#include <stdio.h>

int main (void)
{
  int N, M, start, end, save;
  scanf("%d %d", &N, &M);
  int BascketNum[N];
  for(int i = 0; i < N; i++)
    BascketNum[i] = i + 1;
  for(int i = 0; i < M; i++)
    {
      scanf("%d %d", &start, &end);
      for (; start < end; start++)
        {
          save = BascketNum[start - 1];
          BascketNum[start - 1] = BascketNum[end - 1];
          BascketNum[end - 1] = save;
          end--;
        }
    }
  for (int z = 0; z < N; z++)
    {
      printf("%d ",BascketNum[z]);
    }
}
```

이 문제는 중간에 바구니를 바꾸는 부분이 약간 난잡하긴 했지만, 의외로 쉽게 풀렸던 문제이다.

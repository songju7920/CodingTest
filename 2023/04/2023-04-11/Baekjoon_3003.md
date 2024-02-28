## 백준 3003번  킹, 퀸, 룩, 비숍, 나이트, 폰

풀이 코드 :
```jsx
#include <stdio.h>

int main (void)
{
  int Cnt[6];
  for(int i = 0; i < 6; i++)
    scanf("%d", &Cnt[i]);
    printf("%d %d %d %d %d %d", 1 - Cnt[0], 1 - Cnt[1], 2 - Cnt[2], 2 - Cnt[3], 2 - Cnt[4], 8 - Cnt[5]);
}
```

다른사람의 코드 :

```jsx
#include <stdio.h>

int main()
{   
    int chess[6] = {1,1,2,2,2,8};
    int input[6];
    int result[6];

    for(int i = 0; i < 6; i++){
        scanf("%d", &input[i]);
        result[i] = chess[i] - input[i];
    }

    for(int i = 0; i < 6; i++){
        printf("%d ", result[i]);
    }
    
    return 0;
}
```

배열과 반복문을 사용하여 가독성이 매우 좋지만, 최적화가 떨어지는 문제점이 있었다.

## 백준 2738번 행렬 덧샘

- 문제 해결 과정
    
    반환해야 하는 값 : 첫째 줄부터 N개의 줄에 행렬 A와 B를 더한 행렬을 출력
    
    1. N과 M을 입력받은후 A,B를 이차원 배열로 선언한다
    2. 중첩 반복문을 이용하여 A,B배열을 각각 입력받는다.
    3. 중첩 반복문을 이용하여 A,B배열을 더한 값을 출력한다

풀이 코드 :

```tsx
#include <stdio.h>

int main(void) {
  int N, M;
  scanf("%d %d",&N ,&M);
  int Num1[N][M], Num2[N][M];
  
  for(int i = 0; i < N; i++)
    for(int j = 0; j < M; j++)
      scanf("%d",&Num1[i][j]);
  
  for(int i = 0; i < N; i++)
    for(int j = 0; j < M; j++)
      scanf("%d",&Num2[i][j]);
  
  for(int i = 0; i < N; i++) {
      for(int j = 0; j < M; j++)
        printf("%d ",Num1[i][j] + Num2[i][j]);
      printf("\n");
    }
}
```

이번 문제는 2차원 배열이라는 개념과 중첩반복문을 정확하게 숙지하고 있다면 아주 쉽게 풀수 있는 문제였다.

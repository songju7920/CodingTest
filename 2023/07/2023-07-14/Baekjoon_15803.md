## 백준 15803 **PLAYERJINAH’S BOTTLEGROUNDS**

- 문제 해결과정
  - 반환해야 하는 값 : 3개의 좌표가 주어졌을 때 그 점들이 일직선 상에 위치하는지 계산해서 출력
  1. 각 플래이어의 좌표 받기.
  2. 각 점끼리의 직선방정식의 기울기 구하기
  3. 모든 기울기가 같다면 “WHERE IS MY CHICKEN?”을, 아니면 "WINNER WINNER CHICKEN DINNER!"을 출력

풀이 코드 :

```jsx
#include <stdio.h>

int main() {
  int playerPOS[2][3];

  for (int i = 0; i < 3; i++) {
    scanf("%d %d", &playerPOS[0][i], &playerPOS[1][i]);
  }

  int cal1 = playerPOS[0][0] - playerPOS[0][1];
  int cal2 = playerPOS[1][0] - playerPOS[1][1];
  double inclination1 = (double)cal1 / cal2;
  if(cal1 == 0 || cal2 == 0){
    inclination1 = 0;
  }

  cal1 = playerPOS[0][2] - playerPOS[0][1];
  cal2 = playerPOS[1][2] - playerPOS[1][1];
  double inclination2 = (double)cal1 / cal2;
  if(cal1 == 0 || cal2 == 0){
    inclination2 = 0;
  }

  cal1 = playerPOS[0][2] - playerPOS[0][0];
  cal2 = playerPOS[1][2] - playerPOS[1][0];
  double inclination3 = (double)cal1 / cal2;
  if(cal1 == 0 || cal2 == 0){
    inclination3 = 0;
  }

  if (inclination1 == inclination2 && inclination1 == inclination3) {
    printf("WHERE IS MY CHICKEN?");
  } else {
    printf("WINNER WINNER CHICKEN DINNER!");
  }
}
```

이 문제는 같은 직선에 위치한 점들은 기울기가 같다는 점을 이용하여 풀었고, 반례 찾느라 시간을 많이 썼던 문제였다.

- 새로 알게된점
  C언어에서는 0으로 정수를 나누는 것이 불가하고, 0으로 실수를 나누면 -inf, inf가 된다.

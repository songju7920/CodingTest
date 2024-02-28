## 백준 25206번 너의 평점은

문제 해결 과정

반환해야 하는 값 : 전공평점을 출력한다

1. 20번만큼 다음 내용을 반복한다 :
    1. 과목명(string) 학점(double) 등급(char)입력 받는다.
    2. 등급별로 과목 평점을 구한다(등급이 P면 계산에서 제외한다)
    3. (학점 * 과목평점) / 학점 을 계산한다
    4. 결과를 출력한다

풀이 코드 :

```tsx
#include <stdio.h>
#include <string.h>

int main(void) {
  char Rating[3], SubjectName[51];
  float Grade, result = 0, sum = 0;

  for (int i = 0; i < 20; i++) {
    scanf("%s %f %s", SubjectName, &Grade, Rating);
    if(strcmp(Rating, "P") != 0)
      sum += Grade;
    if (strcmp(Rating, "A+") == 0)
      result += Grade * 4.5;
    else if (strcmp(Rating, "A0") == 0)
      result += Grade * 4.0;
    else if (strcmp(Rating, "B+") == 0)
      result += Grade * 3.5;
    else if (strcmp(Rating, "B0") == 0)
      result += Grade * 3.0;
    else if (strcmp(Rating, "C+") == 0)
      result += Grade * 2.5;
    else if (strcmp(Rating, "C0") == 0)
      result += Grade * 2.0;
    else if (strcmp(Rating, "D+") == 0)
      result += Grade * 1.5;
    else if (strcmp(Rating, "D0") == 0)
      result += Grade * 1.0;
    else
      result += Grade * 0.0;
  }
  
  printf("%f", result / sum);
  return 0;
}
```

이번 문제는 로직을 순서대로 구현할려 노력했지만, P를 구별해 처리하는 코드를 빠트려 괜한 시간만 낭비했던 문제였다. 앞으로는 더 철저히 로직을 새우고 반례도 열심히 생각해야겠다고 느낀 문제였다.

- 알게된점
    - strcmp문
        
        문자열이 해당 문자와 일치하는지 확인하고 같으면 0, 다르면 1을 출력한다.
        
        예제
        ```tsx
        printf("당신의 접속코드?");
        scanf("%s",userCode);
        if(strcmp(userCode, "관리자 코드") == 0)
          printf("관리자 계정에 로그인 되었습니다.");
        else
          printf("코드가 다릅니다.");
        ```

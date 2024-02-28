## 백준 2745 진법변환

- 문제 해결과정

  - 반환해야 하는 값 : n진수 수가 주어질때, 10진수로 변환하여 출력하라.

  1. 입력받기
     1. 공백이 입력되면 반복문 탈출
     2. 수인지 문자인지 파악후 계산하기 위해 변환시켜서 저장한다.
     3. 길이를 파악하기위한(뒤에서부터 곱해야 함으로 길이가 필요) length를 1올린다
  2. 계산하기

     1. 뒤에서부터 n의 m제곱을 곱해 sum에 더해준다

        ex) 10010 → 0 _ (2^0) + 1 _ (2^1) + 0 _ (2^2) + 0 _ (2^3) + 1 \* (2^4)

  3. sum을 출력한다

풀이 코드 :

```jsx
#include <stdio.h>

int main() {
  int n, sum = 0, square = 1, length = -1;
  char numbers[1000];

  //입력받기
  for (int i = 0;; i++) {
    scanf("%c", &numbers[i]);
    if (numbers[i] == 32) break;

    if (numbers[i] > 64) numbers[i] -= 55;
    else numbers[i] -= 48;
    length++;
  }
  scanf("%d", &n);

  //계산
  for (int i = length; i > -1; i--) {
    sum += numbers[i] * square;
    square *= n;
  }
  printf("%d", sum);
}
```

이 문제는 진수에 대한 이해도가 기본적으로 필요하고 ascii코드의 대한 이해도 필요로 하던 문제였지만 차근차근 풀면 충분히 풀수 있는 문제였다고 생각한다.

- 다른사람의 풀이

  ```jsx
  include <stdio.h>
  #include <string.h>
  #include <math.h>

  int main(){
      int b, a=0;
      char n[31];
      scanf("%s %d", &n, &b);
      for(int i=0; i<strlen(n); i++){
          if(n[strlen(n)-1-i]>64)
              a += pow(b, i)*(n[strlen(n)-1-i]-55);
          else
              a += pow(b, i)*(n[strlen(n)-1-i]-48);
      }
      printf("%d", a);
      return 0;
  }
  ```

  이분은 math.h의 pow함수를 이용하여 거듭제곱을 쉽게 만들었고, 계산할때 Ascii코드값을 변환시킨것이 인상깊은 풀이였다. 이분처럼 나도 앞으로 더욱 함수와 이렇게 시간복잡도를 줄일수 있는 로직을 생각해내는것이 중요할것 같다고 생각했다.

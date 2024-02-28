## 백준 1157 단어공부

- 문제 해결 과정
    1. 알파벳 대소문자로 이루어진 단어를 입력받는다.
    2. 각 알파벳이 몇개가 나왔는지 Cnt한다
        1. 소문자는 대문자로 바꿔 판별한다.
    3. 비교하면서 나온적이 제일 많은 알파벳을 찾는다 (다른사람 풀이 참고해서 보충)
        1. Cnt값들을 비교하면서 제일 큰 값을 best에 저장해놓는다
        2.  만약 같은것이 있다면 result값을 ++한다.
    4. 나온적이 제일 많은 알파벳을 출력한다
        1. 만약 result > 1이면 ?를 출력한다

풀이 코드 :

```tsx
#include <stdio.h>
#include <string.h>

int main(void) {
  int Cnt[27], best = 0, Alpabet = 0, result = 0;
  for(int i = 0; i < 26; i++)
    Cnt[i] = 0;
  char str[1000001];
  scanf("%s", str);
  
  size_t str_len = strlen(str);
  
  for (int i = 0; i < str_len; i++)
    for(int j = 65; j < 91; j++)
      if(str[i] == j || str[i] - 32 == j)
        Cnt[j-65]++;
  
  for (int i = 0; i < 26; i++) {
    if(Cnt[i] > best) {
      best = Cnt[i];
      Alpabet = i + 65;
    }
  }
  for(int i = 0; i < 26; i++)
    if(best == Cnt[i]) {
      result++;
    }
  if(result > 1)
    printf("?");
  else
    printf("%c", Alpabet);
}
```

이번 문제는 문제 해결과정에서의 3번부분의 비교하는 로직을 잘 구현하지 못하였다. 앞으로 비슷한 문제들을 계속 풀어가면서 컴퓨터식 사고방식을 더욱 잘할수있도록 익히고, 문제를 더 세분화한뒤 푸는 연습을 해야겠다.

---

- 알게된점
    
    for문에서 strlen함수를 쓰면 반복때마다 선언되며 무한루프 발생 위험이 있다는 것을 알게되었다. 변수에 저장한후 가져다쓰는것이 더 안전하다는것을 알게되었다.

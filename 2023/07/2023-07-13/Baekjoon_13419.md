## 백준 13419 탕수육

- 문제 해결과정
  - 반환해야 하는 값 : 문자열이 주어졌을때 2개의 간격을 두고 문자열을 반복할수있는 2개의 조합 출력
  1. 테스트 케이스 횟수 받기
  2. 테스트 케이스 횟수만큼 반복
     1. 문자열 입력 받기
     2. 문자열의 길이만큼 순회하면서 짝수 인덱스는 answer2에 홀수 인덱스에선 answer 1에 저장
     3. 만약 문자열 길이가 홀수면 answer1에 짝수 인덱스, answer2엔 홀수 인덱스 넣기
  3. 결과 출력

풀이 코드 :

```jsx
#include <stdio.h>
#include <string.h>

int main() {
  int n;
  scanf("%d", &n);

  for (int i = 0; i < n; i++) {
    char answer1[55] = {0};
    char answer2[55] = {0};
    char str[27] = {0};
    int idx = 0;
    scanf("%s", str);

    for (int j = 0; j < strlen(str); j++) {
      answer1[idx] = str[j];
      j++;
      answer2[idx] = str[j];
      idx++;
    }
    idx--;

    if (strlen(str) % 2 != 0) {
      for (int j = 0; j < strlen(str); j++) {
        answer2[idx] = str[j];
        j++;
        idx++;
        answer1[idx] = str[j];
      }
    }

    printf("%s\n", answer1);
    printf("%s\n", answer2);
  }
}
```

이 문제는 null문자 처리때문에 매우 어려웠다. idx값 조정을 잘못해서 null문자가 중간에 자꾸 들어가서 애를 좀 먹었던 문제였다.

- 다른 사람의 풀이
  ```jsx
  #include <stdio.h>
  #include <string.h>

  int main(){
  	char str[30], a[30], b[30];
  	int t, L;
  	scanf("%d",&t);
  	while(t--){
  		scanf("%s",str);
  		L = strlen(str);
  		int j = 0, k = 0;
  		for (int i=0; i<L; i++){
  			if (i%2 == 0)
  				a[j++]=str[i];
  			else
  				b[k++]=str[i];
  		}
  		if (L%2 == 1)
  			for (int i=0; i<L; i++){
  				if (i%2 == 1)
  					a[j++] = str[i];
  				else
  					b[k++] = str[i];
  			}
  	a[j] = b[k] = '\0';
  	printf("%s\n%s\n",a,b);
  	}
  }
  ```
  이 사람의 코드는 조금만 개선하면 가독성이 매우 뛰어날 것 같고, 내 코드보다 로직이 훨씬 간결하다. 이런 로직을 설계할 수 있도록 더욱 노력 해야겠다.

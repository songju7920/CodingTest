## 백준 1449번 **수리공 항승**

- 문제 해결과정
  - 반환해야 하는 값 : 배열이 주어질때 서로의 거리 + 1이 L보다 작은 묶음의 수를 구하여 반환하라.
  1. N, L를 받고, arr를 정의한다.
  2. 선택정렬 알고리즘을 사용하여 오름차순으로 정렬한다.
  3. 앞에서부터 뒤에 있는 구멍들과 거리를 비교하며 동시에 테이프로 덮을 수 있다면 덮는다.

풀이 코드 :

```jsx
#include <stdio.h>
#include <string.h>
int arr[1000];

void sort(int *arr, int N) {
  for (int i = 0; i < N - 1; i++) {
    int min = i;
    for (int j = i + 1; j < N; j++) {
      if (arr[min] > arr[j])
        min = j;
    }
    int temp = arr[min];
    arr[min] = arr[i];
    arr[i] = temp;
  }
}

int main(void) {
  int N, L;
  int answer = 0;
  scanf("%d %d", &N, &L);
  for (int i = 0; i < N; i++) {
    scanf(" %d", &arr[i]);
  }

  sort(arr, N);

  for (int i = 0; i < N; i++) {
    int cnt = 0;

    for (int j = i + 1; j < N; j++) {
      if (arr[j] - arr[i] + 1 <= L) {
        cnt++;
        continue;
      } else {
        break;
      }
    }

    answer++;
    i += cnt;
  }

  printf("%d", answer);
}
```

이 문제는 정렬까진 쉬웠지만 후반 그리디 알고리즘을 사용할때 실력이 부족해 조금 고전했던 문제다.

- 다른사람의 풀이
  ```jsx
  #include <stdio.h>
  #include <stdlib.h>

  int main() {
  	int n, l, count = 0;
  	scanf("%d %d", &n, &l);
  	int* pipe = (int*)calloc(1000, sizeof(int));
  	for (int i = 0; i < n; i++) {
  		int tmp;
  		scanf("%d", &tmp);
  		pipe[tmp - 1] = 1;
  	}

  	int cor_index = 0, remaining_l = 0;
  	while (cor_index < 1000) {
  		if (pipe[cor_index++] != 0 || remaining_l != 0) {
  			if (remaining_l > 0) remaining_l--;
  			else {
  				count++;
  				remaining_l = l - 1;
  			}
  		}
  	}

  	printf("%d\n", count);
  }
  ```
  이사람은 정렬과 그리디 알고리즘을 나보다 훨씬 더 가독성 좋게 작성하였다.

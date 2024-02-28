## 백준 10812번 바구니 순서 바꾸기

- 문제 해결 과정
    - 반환해야 하는 값 : 모든 순서를 회전시킨후, 가장 왼쪽 바구니의 숫자부터 공백으로 구분해 출력한다.
    1. N과 M을 입력받는다.
    2. M의 값만큼 반복한다
        1. begin,end,mid를 입력받아 저장한다.
        2. cmp1의 값을 맨 앞에 와야하는 basketNum배열의 인덱스로 정한다.
        3. basketNum[begin - 1] == cmp1일때까지 반복
            1. basketNum배열의 값들을 회전시킨다.
    3. 값을 출력 한다

풀이 코드 :

```c
#include <stdio.h>
#include <string.h>

int main(void) {
  int N, M, begin, mid, end, save, cmp1, cmp2;

  scanf("%d %d", &N, &M);
  int basketNum[101];

  for (int i = 0; i < N; i++)
    basketNum[i] = i + 1;

  for (int i = 0; i < M; i++) {
    scanf("%d %d %d", &begin, &end, &mid);
    cmp1 = basketNum[mid - 1];
    for (int j; basketNum[begin - 1] != cmp1; j++) {
      cmp2 = basketNum[end - 1];
      for (int k = begin; basketNum[begin - 1] != cmp2; k++) {
        save = basketNum[begin - 1];
        basketNum[begin - 1] = basketNum[k];
        basketNum[k] = save;
      }
    }
  }

  for (int i = 0; i < N; i++)
    printf("%d ", basketNum[i]);
}
```

이 문제는 로직 설계 및 구현이 어려웠던 문제였다. 기본적으로 배열과 배열 순서 변경에 대한 이해를 필요로 하여 꽤나 고전했던 문제였음에도 불구하고 난이도가 낮은 편에 속해 아직도 내가 많이 부족하다는 것을 다시 느끼게 되었다.

다른사람의 풀이

```c
#include <stdio.h>

int main()
{
	int arr[100];
	int temp[100];
	int n, m;
	int a, b, c;

	scanf("%d %d", &n, &m);

	for (int i = 1; i <= n; i++) {
		arr[i] = i;
	}

	for (int i = 1; i <= m; i++) {
		int cnt = 1;
		scanf("%d %d %d", &a, &b, &c);
    //mid부터 end까지 반복하는 반복문
		for (int j = c; j <= b; j++) {
      //temp[cnt]에 = arr[j]를 저장
			temp[cnt] = arr[j];
			cnt++;
		}
    //start부터 mid-1까지 반복하는 반복문
		for (int k = a; k <= c -1; k++) {
      //temp[cnt]에 = arr[k]를 저장
			temp[cnt] = arr[k];
			cnt++;
		}

		cnt = 1;

    //temp의 값을 arr배열에 복사하는 반복문
		for (int z = a; z <= b; z++) {
			arr[z] = temp[cnt];
			cnt++;
		}
	}

	for (int i = 1; i <= n; i++) {
		printf("%d ", arr[i]);
	}
```

위 코드는 계산용 배열을 따로 만들어 코드를 풀었다. 이 코드가 나의 코드보다 나은 이유는 다음과 같다.

- 가독성 : 다른사람이 읽을때 위 코드가 내 코드보다 이해하기 쉽다.
- 시간복잡도 : 내 코드의 시간복잡도가 위 코드의 시간복잡도보다 크다.

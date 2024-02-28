## 백준 2908번 상수

풀이 코드 :

```jsx
#include <stdio.h>

int main(void) {
  char Num1[4], Num2[4], greater[3];

  scanf("%s %s",Num1, Num2);

  for (int i = 2; i >= 0; i--)
    if (Num1[i] > Num2[i]) {
      for (int j = 2; j >= 0; j--)
        printf("%c", Num1[j]);
      break;
    } else if (Num1[i] < Num2[i]) {
      for (int j = 2; j >= 0; j--)
        printf("%c", Num2[j]);
      break;
    }
  return 0;
}
```

- 풀이 과정
    - return
        
        입력받은 두 수를 뒤집어 그 크기를 비교하고 그중 큰것을 return한다
        
    1. 두 수를 string형태로 입력받는다.
    2. 두 수를 역순으로 비교
    3. 문자열 순서 바꿔 출력

이번 문제는 배열의 크기 때문에 계속 오류가 났던 코드이다. 이에 대한 자세한 설명은 밑의 “알게된점”에 적혀있다.

다른사람의 코드 :

```jsx
#include <stdio.h>
#include <string.h>

int main()
{
	int a, b, ra = 0, rb = 0;
	scanf("%d %d", &a, &b);

	ra = ((a % 10) * 100) + ((a / 10) % 10) * 10 + (a / 100);
	rb = ((b % 10) * 100) + ((b / 10) % 10) * 10 + (b / 100);

	if (ra > rb)
	{
		printf("%d\n", ra);
	}
	else
	{
		printf("%d\n", rb);
	}
	
	return 0;
}
```

위 코드는 string형을 사용하지 않고 int형으로 사칙연산자와 if문을 사용하여 풀이 했다. 결론적으론 반복문을 쓰지 않아 위 코드가 최적화가 더 잘되어 있긴 하다.

- 알게된점
    
    배열을 선언할때 1만큼의 여유공간을 너 넣어놓아야 안전하다는것을 깨달았다.
    
    예를들어, "234"는 char[3] 배열에도 저장이 가능하다. 그러나 이는 예상치 못한 문제가 발생할 가능성이 있는 위험한 코드라는것이다. char[3] 배열에 "234"와 같은 3자리 문자열을 저장하게 되면, 해당 배열의 마지막에는 NULL 문자가 자동으로 삽입되지 않아서 이후에 해당 배열에 접근할 때, 예상치 못한 결과가 발생할 가능성이 있다. 예를 들어, 문자열 처리 함수를 사용할 때 NULL 문자를 찾지 못하면, 예상치 못한 동작을 할 수 있다.

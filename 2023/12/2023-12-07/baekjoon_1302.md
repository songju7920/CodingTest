## 백준 1302번 **베스트셀러**

### 문제 해결과정

- 문제 분류 : 자료구조, 문자열, 정렬, 해시
- 반환해야 하는 값 : 가장 많이 팔린 책의 이름을 출력하라
- 풀이과정
  1. 풀이과정

### 풀이 코드

```jsx
n = int(input())
bookList = []
soldedCnt = []
results = []

for i in range(n):
  book = input()
  try:
    idx = bookList.index(book)
    soldedCnt[idx] += 1
  except:
    bookList.append(book)
    soldedCnt.append(1)

maxCnt = max(soldedCnt)
for i in range(len(bookList)):
  if soldedCnt[i] == maxCnt: results.append(bookList[i])

print(min(results))
```

코드 시간복잡도 (빅오) : O(n)

한줄 회고 : 이 문제는 생각보다 간단했지만, 자료형을 잘못 선택해 아쉬웠던 문제였다.

### 다른사람의 풀이

```jsx
N = int(input())

book = {}
for i in range (0,N):
    i = input()
    if (i in book) == False:
        book[i] = 1
    else:
        book[i] += 1

sale = list(book.items())

max = 0
best= []
for i in range(0,len(sale)):
    if max < sale[i][1]:
        max = sale[i][1]

for i in range(0,len(sale)):
    if sale[i][1] == max:
        best.append(sale[i][0])
best.sort()

print(best[0])
```

이 코드를 보면 내가 가장 아쉬웠던 점중 하나인 자료형을 적절하게 잘 사용한것을 알 수 있다. 난 책의 이름과 팔린 횟수를 따로따로 배열에 저장하였으나, 이 코드는 딕셔너리를 이용하여 코드를 깔끔하게 작성하였다.

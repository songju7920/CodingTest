# 2166 Beakjoon

생성일: 2024년 2월 7일 오후 1:28

## 프로그래머스 2166번 **다각형의 면적**

### 문제 해결과정

- 문제 분류 : 기하학
- 반환해야 하는 값 : 다각형의 좌표가 주어졌을때, 면적을 구하여라.
- 풀이과정
    1. 입력값 받기
    2. 신발끈 공식을 이용하여 공식 도출
    3. 결과의 절대값을 소숫점 첫째 자리까지 반올림

### 풀이 코드

```python
import sys
input = sys.stdin.readline

N = int(input())
points = [list(map(int, input().split())) for _ in range(N)]
points.append(points[0])

answer = 0
for i in range(N):
  answer += points[i][0] * points[i + 1][1]
  answer -= points[i][1] * points[i + 1][0]

print(round(abs(answer / 2), 1))
```

코드 시간복잡도 (빅오) : O(n)

질문창 또는 블로그 참고: O

한줄 회고 : 이번 문제는 수학적 지식이 요구되는 문제였다. 아무래도 내가 기하학쪽 알고리즘을 잘 못풀었다 보니, 앞으로 기하학쪽 알고리즘을 열심히 풀어야겠다고 생각했다.

### 새로 알게된점

- 신발끈 공식
    
    ![https://mblogthumb-phinf.pstatic.net/MjAyMTA5MDlfNzUg/MDAxNjMxMTc0OTY1Nzk2.Z5qa5Mjnv7Tnsy6wTlLy_iH4f-HztcniNjcTEE4P08Qg.FM4O0VfkW5sPpG2HWkQM-FcZuO9S91aycVw8BdVMeYEg.JPEG.jjangting/%EC%84%B8%EC%A0%90%EC%95%8C%EB%95%8C%EB%84%93%EC%9D%B401.jpg?type=w800](https://mblogthumb-phinf.pstatic.net/MjAyMTA5MDlfNzUg/MDAxNjMxMTc0OTY1Nzk2.Z5qa5Mjnv7Tnsy6wTlLy_iH4f-HztcniNjcTEE4P08Qg.FM4O0VfkW5sPpG2HWkQM-FcZuO9S91aycVw8BdVMeYEg.JPEG.jjangting/%EC%84%B8%EC%A0%90%EC%95%8C%EB%95%8C%EB%84%93%EC%9D%B401.jpg?type=w800)
    
    출처: [https://blog.naver.com/jjangting/222500620549](https://blog.naver.com/jjangting/222500620549)
    
    신발끈 공식은 다각형의 꼭짓점의 좌표를 모두 알고 있을때 사용되는 공식으로, 그저 간단하게 X자 모양으로 연결되는 좌표들을 곱해 서로 뺸다음 반으로 나누면 된다. 위에 그림은 삼각형을 예시로 들고있지만, 이 공식은 사각형, 오각형, 육각형등 모든 다각형에 대하여 성립한다.
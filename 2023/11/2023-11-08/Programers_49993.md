## 프로그래머스 49993번 스킬트리

### 문제 해결과정

- 문제 분류 : 탐색, 구현
- 반환해야 하는 값 : 선행 스킬 순서 skill과 유저들이 만든 스킬트리를 담은 배열 skill_trees가 매개변수로 주어질 때, 가능한 스킬트리 개수를 return
- 풀이과정
  1. 스킬트리의 순서를 문자열에서 배열로 변환한다
  2. 스킬트리들을 분리하여 배열로 변환한다.
  3. 만약 스킬트리의 다음 필요한 스킬이 나왔다면 다음 스킬을 가르키는 idx를 지정하게한다.
  4. 만약 건너뛰었다면 다음 스킬트리를 검사하러 간다.

### 풀이 코드

```jsx
function solution(skill, skill_trees) {
  let answer = 0;
  let skills = skill.split("");

  for (let skill_tree of skill_trees) {
    let nextSkill = 0;
    let isPossible = true;
    skill_tree = skill_tree.split("");
    for (let user_skill of skill_tree) {
      if (user_skill == skills[nextSkill]) {
        nextSkill++;
      } else if (skills.indexOf(user_skill) != -1) {
        isPossible = false;
        break;
      }
    }
    if (isPossible) answer++;
  }

  return answer;
}
```

코드 시간복잡도 (빅오) : O(n^2)

한줄 회고 : 이 문제는 시간복잡도를 줄이는 것과, 검사하는 로직이 중요했다.

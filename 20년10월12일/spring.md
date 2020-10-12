# 네트워크(깊이 / 너비 우선탐색)

> 🧷 링크 : https://programmers.co.kr/learn/courses/30/lessons/43162

## [ 문제 ]

### - 문제 설명

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다. 예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때 컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다. 따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때, 네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

### - 제한 사항

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.

- 각 컴퓨터는 0부터 n-1인 정수로 표현합니다.

- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.

- computer[i][i]는 항상 1입니다.

### - 입출력 예

| n   | computers                         | return |
| :-- | :-------------------------------- | :----- |
| 3   | [[1, 1, 0], [1, 1, 0], [0, 0, 1]] | 2      |
| 3   | [[1, 1, 0], [1, 1, 1], [0, 1, 1]] | 1      |

## [ 해결방법 ]

### - 수도코드

1. answer 변수 선언

2. 연결여부 확인할 배열에 컴퓨터의 길이만큼 false값 할당

3. 컴퓨터의 1 index가 1인 경우 => 두번째 컴퓨터와 연결

4. 컴퓨터의 2 index가 1인 경우 => 세번째 컴퓨터와 연결

5. 연결이 끊어지면 answer++

### - 코드

```js
function solution(n, computers) {
  let answer = 0;

  const check = [];
  for (const computer of computers) {
    check.push(false);
  }

  function DFS(index) {
    check[index] = true;
    for (let i = 0; i < computers.length; i++) {
      if (computers[index][i] === 1 && !check[i]) {
        DFS(i);
      }
    }
  }

  for (let i = 0; i < computers.length; i++) {
    if (!check[i]) {
      DFS(i);
      answer += 1;
    }
  }

  return answer;
}
```

n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때, 최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다. 예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

**입출력 예**

| n   | costs                                     | return |
| --- | ----------------------------------------- | ------ |
| 4   | [[0,1,1],[0,2,2],[1,2,5],[1,3,1],[2,3,8]] | 4      |

---

**코드**

```js
function getParent(arr, i) {
  if (arr[i] === i) return i;
  return getParent(arr, arr[i]);
}

function solution(n, costs) {
  costs.sort((x, y) => x[2] - y[2]);
  const arr = [];
  for (var i = 0; i < n; i++) {
    arr[i] = i;
  }
  let acc = 0;
  let cur = 0;
  let branch = 0;
  while (branch < n - 1) {
    const left = costs[cur][0];
    const right = costs[cur][1];
    const lparent = getParent(arr, left);
    const rparent = getParent(arr, right);
    console.log(lparent, rparent);
    if (lparent === rparent) {
      cur++;
      continue;
    }
    arr[rparent] = lparent;
    acc += costs[cur++][2];
    branch++;
  }
  return acc;
}
```

먼저 탐욕법이란 현재상태에서 최선의 결과를 계속 선택해나가는 방법이다.

푼 알고리즘을 살펴본다면

1. 우선 sort 배열 메서드를 사용하여 비용이 가장작은 순서대로 나열하였다.
2. arr이라는 임시 배열을 만든뒤 해당 섬의 개수만큼 인덱스와 같은 값을 넣어 생성해준다.
3. 최소다리연결할 누산기 acc, 현재 인덱스를 나타낼 cur , n개의 섬만큼 while 문을 돌기위한 branch 변수를 만들어준다.
4. while 문을 n개의 섬이 연결될때까지 돌린다.(arr에 모든 섬이 있을때까지)
5. left, rigth로 섬두개를 선언하고 left섬의 부모섬(이미 연결되있다는 뜻),right섬의 부모섬을 찾은뒤 두섬이 같다면 현재인덱스 cur을 올려 다음 조건을 탐색
6. 같지않다면 arr에 오른쪽섬에 왼쪽 섬의 값을 넣어 서로 같게 한다.
7. 또 누산기에 연결비용을 더하고 branch값도 올려준다.

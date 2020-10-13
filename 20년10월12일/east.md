# hashTable

- insert(), retrieve(), remove() 메소드를 가진 해시 테이블을 만드세요.

* resize를 구현하지 않아도 테스트는 통과하지만, 충돌은 처리할 수 있어야 합니다.

```js
const makeHashTable = function () {
  let result = {};
  let storage = []; //[[bucket],[bucket]]
  let storageLimit = 1000;
  result.insert = function (/*...*/ key, value) {
    // TODO: implement `insert()`

    var index = getIndexBelowMaxForKey(key, storageLimit); //index = 정수(0~)
    storage[index] = storage[index] || []; //storage[0] = storage[0] || [];
    var pairs = storage[index];
    var replaced = false;
    for (var i = 0; i < pairs.length; i++) {
      if (pairs[i][0] === key) {
        //링크드리스트
        pairs[i][1] = value;
        replaced = true;
      }
    }

    if (!replaced) {
      pairs.push([key, value]);
    }
  };
  result.retrieve = function (key /*...*/) {
    var index = getIndexBelowMaxForKey(key, storageLimit); //index = 정수(0~)
    var pairs = storage[index];
    if (pairs === undefined) {
      return;
    } else {
      for (let i = 0; i < pairs.length; i += 1) {
        if (pairs[i] !== undefined && pairs[i][0] === key) {
          return pairs[i][1];
        }
      }
    }
  };
  result.remove = function (key /*...*/) {
    var index = getIndexBelowMaxForKey(key, storageLimit); //index = 정수(0~)
    var index = getIndexBelowMaxForKey(key, storageLimit);
    var pairs = storage[index];
    var pair;
    for (var i = 0; i < pairs.length; i++) {
      pair = pairs[i];
      if (pair[0] === key) {
        var value = pair[1];
        delete pairs[i];
        return value;
      }
    }

    // `remove()` 함수를 구현하세요.
  };

  return result;
};

// 이 함수는 "해시 함수" 입니다. 지금은 이 함수에 대해 걱정할 필요가 없습니다.
// 해시 함수는 문자열과 숫자 max를 인자로 받아, 문자열을 0에서 max-1 사이에 분포된 정수로 바꿔 리턴합니다.
const getIndexBelowMaxForKey = function (str, max) {
  let hash = 0;
  for (let i = 0; i < str.length; i++) {
    hash = (hash << 5) + hash + str.charCodeAt(i);
    hash = hash & hash; // Convert to 32bit integer
    hash = Math.abs(hash);
  }
  return hash % max;
};
```

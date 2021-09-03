# 문제
정수를 요소로 갖는 배열과 특정 구간을 입력받아, 해당 구간 내에서 최소값을 리턴해야 합니다.

## 입력
### 인자 1 : arr
* number 타입을 요소로 갖는 배열
* arr.length는 500,000 이하
* arr[i]는 -100,000 이상 100,000 이하의 정수

### 인자 2 : ranges
* number 타입을 요소로 갖는 배열
* ranges.length는 10,000 이하
* ranges[i]는 특정 구간을 의미
* ranges[i][0]은 i번째 구간의 시작 인덱스
* ranges[i][1]은 i번째 구간의 마지막 인덱스

## 출력
* 배열(arr)를 리턴해야 합니다. (입출력 예시 참고)
* arr[i]는 i번째 구간(ranges[i])의 최소값

## 입출력 예시
```javascript
const arr = [1, 3, 2, 7, 9, 11];
const mins = rangeMinimum(arr, [
  [1, 4],
  [0, 3],
]);
console.log(mins); // --> [2, 1]
```

## Advanced
* Advanced1: 주어진 배열에서 특정 구간의 최소값을 구하는 단순한 알고리즘은 단순 순회(O(N))입니다. 같은 배열에 대해서 다양한 구간에 대한 최소값을 구할 경우, 단순 순회는 O(N^2) 입니다(구간의 개수도 N개라 가정할 경우). 적절한 자료구조를 통해 이와 같은 구간 조회에 대한 반복 작업을 효율적(O(N * logN))으로 수행할 수 있습니다. 구간 트리(segment tree)에 대해서 학습하시고, Advanced 테스트 케이스를 통과해 보시기 바랍니다.
* 트리를 객체 또는 배열로 구현할 수 있습니다. 객체로 구현하는 것이 보다 직관적이기 때문에 객체로 먼저 도전하시기 바랍니다. 레퍼런스는 모두 주어집니다.
* 구간의 최대값, 합도 동일한 로직으로 구현하면 됩니다.

## 문제풀이
```javascript
// 구간 트리 : Segment Tree
// 구간 트리는 객체(배열)을 절반으로 나눠 결국 한 요소만 남을 때까지 반복해서 저장한다.

// naive solution: O(N) (search only)
// const rangeMinimum = function (arr, ranges) {
//   return ranges.map((range) => {
//     const [start, end] = range;
//     let min = Number.MAX_SAFE_INTEGER;
//     for (let i = start; i <= end; i++) {
//       if (arr[i] < min) min = arr[i];
//     }
//     return min;
//   });
// };

// solution with segment tree: O(logN) (search only)
// object implementaion
const rangeMinimum = function (arr, ranges) {
  // ts: tree start. te: tree end
  // arr의 ts부터 te까지를 tree로 만든다.
  const createMinTree = (arr, ts, te) => {
    // base case
    if (ts === te) { // 시작점과 마지막점이 동일해지면
      return { value: arr[ts] }; // 만들어진 트리를 리턴
    }

    // recursive case
    // 현재 범위를 절반을 기준으로 왼쪽과 오른쪽으로 나눈다
    const mid = parseInt((ts + te) / 2);
    const left = createMinTree(arr, ts, mid);
    const right = createMinTree(arr, mid + 1, te);

    return {
      value: Math.min(left.value, right.value), // left,right값 중 작은 값을 저장(최솟값을 구하고 있으므로)
      left,
      right,
    };
  };
  const tree = createMinTree(arr, 0, arr.length - 1);
  
  // 범위를 입력 받는다. rs: range start, re: reange end
  const findMin = (ts, te, rs, re, tree) => {
    // base case 현재 tree와 구간이 정확히 일치하거나
    // 구간이 tree를 포함할 경우
    if (rs <= ts && te <= re) {
      return tree.value; //1번(최초) 노드의 값을 리턴
    }

    // 현재 tree에 주어진 구간이 겹치지 않는 경우
    if (te < rs || re < ts) {
      return Number.MAX_SAFE_INTEGER; // 임의의(약속된) 값을 리턴
    }

    // 겹치는 부분이 존재하는 경우
    const mid = parseInt((ts + te) / 2);
    return Math.min(
      findMin(ts, mid, rs, re, tree.left), //
      findMin(mid + 1, te, rs, re, tree.right)
    );
  };

  // 인자 range : 여러 특정 
  const mins = ranges.map((range) => {
    const [start, end] = range;
    return findMin(0, arr.length - 1, start, end, tree);
  });
  return mins;
};
```

# 문제
정수를 요소로 갖는 배열을 입력받아 오름차순으로 정렬하여 리턴해야 합니다.

## 입력
### 인자 1 : arr
number 타입을 요소로 갖는 배열
arr[i]는 정수
arr.length는 100,000 이하

## 출력
number 타입을 요소로 갖는 배열을 리턴해야 합니다.
배열의 요소는 오름차순으로 정렬되어야 합니다.
arr[i] <= arr[j] (i < j)

## 주의사항
퀵 정렬을 구현해야 합니다.
arr.sort 사용은 금지됩니다.
입력으로 주어진 배열은 중첩되지 않은 1차원 배열입니다.

## 입출력 예시
```javascript
let output = quickSort([3, 1, 21]);
console.log(output); // --> [1, 3, 21]
```

## Advanced
quickSort 함수의 두 번째 인자로 callback 함수를 받아서, 그 함수의 리턴값을 기준으로 요소들을 정렬해 보세요.

## 문제풀이
```javascript
const quickSort = function (arr, callback = (item) => item) { // 콜백함수를 적용한 아이템들의 값을 가지고 정렬
  if (arr.length <= 1) return arr;

  let pivot = arr[0];
  let left = [];
  let right = [];

  for (let i = 1; i < arr.length; i++) {
    if (callback(arr[i]) <= callback(pivot)) {
      left.push(arr[i]);
    } else {
      right.push(arr[i]);
    }
  }

  let leftQuick = quickSort(left, callback);
  let rightQuick = quickSort(right, callback);
  return [...leftQuick, pivot, ...rightQuick];
};

// 퀵 정렬은 분할 정복 방법을 통해 리스트를 정렬한다. (위키백과)
// 1. 리스트 가운데서 하나의 원소를 고른다. (일반적으로 좌측)
// 2. 피벗 앞에는 피벗보다 값이 작은 모든 원소들이 오고, 피벗 뒤에는 피벗보다 값이 큰 모든 원소들이 오도록 피벗을 기준으로 리스트를 둘로 나눈다.
// 3. 분할 된 두 개의 작은 리스트에 대해 재귀적으로 이 과정을 반복한다.
// 4. baseCase는 리스트의 크기가 0이나 1이 될 때까지 이다.

// 1. 배열의 길이가 1과 같거나 작을 경우 배열을 바로 리턴한다.
// 2. 리스트 가운데 하나의 요소를 고르고 pivot이라고 한다. (첫번째 인덱스 할당)
// 3. 배열을 순회하여 pivot을 제외한 모든 요소를 탐색해 pivot보다 작으면 left, 크면 right 배열에 넣는다.
//    => left = [], right = []
//    => arr.length만큼 반복
// 4. left와 rightdp 값을 모두 넣었다면, 각각의 배열에 quickSort를 재귀하여 다시 정렬한다.
// 5. left, pivot, right를 배열에 모두 합쳐 리턴한다.
```

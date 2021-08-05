# 문제
정수를 요소로 갖는 배열을 입력받아 오름차순으로 정렬하여 리턴해야 합니다.

## 입력
### 인자 1 : arr
number 타입을 요소로 갖는 배열
arr[i]는 정수
arr.length는 1,000 이하

## 출력
number 타입을 요소로 갖는 배열을 리턴해야 합니다.
배열의 요소는 오름차순으로 정렬되어야 합니다.
arr[i] <= arr[j] (i < j)

## 주의사항
삽입 정렬을 구현해야 합니다.
arr.sort 사용은 금지됩니다.
입력으로 주어진 배열은 중첩되지 않은 1차원 배열입니다.

## 입출력 예시
```javascript
let output = insertionSort([3, 1, 21]);
console.log(output); // --> [1, 3, 21]
```

## Advanced
insertionSort 함수의 두 번째 인자로 callback 함수를 받아서, 그 함수의 리턴값을 기준으로 요소들을 정렬해 보세요.

## 문제풀이
```javascript
const insertionSort = function (arr, cb = (item) => item) {
  for(let i = 1; i < arr.length; i++) {
    let cur = arr[i]; // 현재 값
    let left = i - 1; // 1 - 0 = 0, 앞의 값을 보도록 설정

  // 나의 앞에 값이 현재 값보다 클 경우 while문 돌기
  while (left >= 0 && cb(arr[left]) > cb(cur)) {
    arr[left + 1] = arr[left]; // 0 + 1 = 1, 나의 뒷 값 위치에 나를 넣어주고
    left --; // 0 - 1 = -1, left 값을 줄여줘서 앞의 값에 접근할 수 있도록 하고
  }
    arr[left + 1] = cur; // 작았던 앞의 값을 나의 앞에 넣어주도록
  }
  return arr;
};

// 삽입 정렬?
// 정렬된 부분과 정렬되지 않는 부분으로 나눠 해당 요소가 정렬된 부분보다 값이 작다면 요소 교환을 실행하는 알고리즘
// 즉, 왼쪽에서 오른쪽으로 가면서 각 요소들을 왼쪽 요소들과 비교하여 알맞은 자리에 삽입하는 형식의 정렬 방법이다. 

// <reference>
// 1. 결과 배열을 하나 만들고 0번째 인덱스를 넣는다. (정렬 기준)
// 2. for loop (1부터 순회)
// 3. 배열의 인덱스 -1 요소보다(left) 높다면 그냥 push
// 4. 아니면, 결과 배열을 0번째 인덱스부터 순회하여 자기 자리 찾기(정렬되어 있기에)
// 5. 자기자리를 찾으면, slice를 통해 요소가 들어갈 왼쪽과 오른쪽을 나누고 concat으로 해당요소를 삽입하여 정렬된 배열을 만든다
```

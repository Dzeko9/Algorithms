# 문제
정수를 요소로 갖는 배열을 입력받아 3개의 요소를 곱해 나올 수 있는 최대값을 리턴해야 합니다.

## 입력
### 인자 1 : arr
number 타입을 요소로 갖는 임의의 배열

## 출력
number 타입을 리턴해야 합니다.

## 주의사항
입력으로 주어진 배열은 중첩되지 않은 1차원 배열입니다.
배열의 요소는 음수와 0을 포함하는 정수입니다.
배열의 길이는 3 이상입니다.

## 입출력 예시
```javascript
let output = largestProductOfThree([2, 1, 3, 7]);
console.log(output); // --> 42 (= 2 * 3 * 7)

output = largestProductOfThree([-1, 2, -5, 7]);
console.log(output); // --> 35 (= -1 * -5 * 7)
```

## 문제풀이
```javascript
const largestProductOfThree = function (arr) {
  const sortedArr = arr.sort((a, b) => (a - b)); // 정렬
  const len = sortedArr.length;
  
  // 3개의 요소 곱하기
  const case1 = sortedArr[len - 1] * sortedArr[len - 2] * sortedArr[len - 3]

  // 음수 * 음수일 경우
  const case2 = sortedArr[len - 1] * sortedArr[0] * sortedArr[1] 

  // 최댓값 3개 곲하기
  return Math.max(case1, case2);
};

// 배열의 길이가 3이면 다 곱함
// 배열의 길이가 4이면 가장 큰 수 순서대로 3개 곱함

// 오름차순으로 정렬해서 비교해준다
// 음수 * 음수가 나올 경우를 고려한다 => 정렬된 상태에서 가장 작은 두 수를 곱하는 것이 양수로 치환되어 가장 큰 값을 곱하는 것
// arr[0] * arr[1] * arr[arr.length - 1]
```

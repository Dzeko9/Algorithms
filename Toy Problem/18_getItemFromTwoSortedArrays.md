# 문제
길이가 m, n이고 오름차순으로 정렬되어 있는 자연수 배열들을 입력받아 전체 요소 중 k번째 요소를 리턴해야 합니다.

## 입력
### 인자 1 : arr1
자연수를 요소로 갖는 배열
arr1.length는 m

### 인자 2 : arr2
자연수를 요소로 갖는 배열
arr2.length는 n

### 인자 3 : k
number 타입의 0 이상의 정수

## 출력
number 타입을 리턴해야 합니다.

## 주의사항
두 배열의 길이의 합은 1,000,000 이하입니다.
어떤 배열 arr의 k번째 요소는 arr[k-1]을 의미합니다.

## 입출력 예시
```javascript
let arr1 = [1, 4, 8, 10];
let arr2 = [2, 3, 5, 9];
let result = getItemFromTwoSortedArrays(arr1, arr2, 6);
console.log(result); // --> 8

arr1 = [1, 1, 2, 10];
arr2 = [3, 3];
result = getItemFromTwoSortedArrays(arr1, arr2, 4);
console.log(result); // --> 3
```

## Advanced
단순히 처음부터 끝까지 찾아보는 방법(O(K)) 대신 다른 방법(O(logK))을 탐구해 보세요.

## 힌트
이진 탐색(binary search)을 응용하여 해결합니다.

## 문제풀이
```javascript
const getItemFromTwoSortedArrays = function (arr1, arr2, k) {
  // 인덱스 값 설정
  let left = 0;
  let rigtht = 0;

  while(k > 0) { // k의 값이 음수가 될때까지
    let count = Math.ceil(k / 2);
    let leftIdx = count; // left(arr1)의 count 할당량(k/2)
    let rightIdx = count; // right(arr2)의 count 할당량(k/2)

    // edge case (이진탐색)
    // 현재 요소가 arr1(arr2)의 끝에 도달했을 때, 남아있는 k를 right, left(arr2, arr1)에 배분
    if (left === arr1.length) {
      right = right + k;
      break;
    if (right === arr2.length) {
      left = left + k;
      break
    }

    // 현재 남아있는 count보다, 남아있는 요소가 적을 경우, rightIdx, leftIdx을 남아있는 요소들의 개수로 바꿔줌
    if (count > arr1.length - left) leftIdx = arr1.length - left;
    if (count > arr2.length - right) rightIdx = arr2.length - right;

    // count 탐색
    // 두 배열의 현재 요소에서 진행해야 하는 count 수를 합친 index값 비교
    if (arr1[left + leftIdx - 1] < arr2[right + rightIdx - 1]) {
      left = left + leftIdx;
      k = k - rightIdx;
    } else {
      right = right + rightIdx;
      k = k - rightIdx;
    }
  }
  leftMax = arr1[leftIdx - 1] || -1;
  rightMax = arr2[rightIdx - 1] || -1;

  return Math.max(leftMax, rightMax)
};

// native solution
//   let count = 0;
//   let left = 0;
//   let right = 0;
//   let target;

//   while(k > count) {
//     if (arr1[left] < arr2[right]) {
//       target = arr1[left];
//       left++;
//     } else {
//       target = arr2[right];
//       right++;
//     }
//     count++;
//   }
//   return target;
// }

// 두 배열을 합쳐 정렬시킨 다음 k-1의 인덱스를 찾자 => kiiled 
```

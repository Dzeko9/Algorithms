# 문제
부분적으로 오름차순 정렬된 정수의 배열(rotated)과 정수(target)를 입력받아 target의 인덱스를 리턴해야 합니다.

+ 부분적으로 정렬된 배열: 배열을 왼쪽 혹은 오른쪽으로 0칸 이상 순환 이동할 경우 완전히 정렬되는 배열
+ 예시: [4, 5, 6, 0, 1, 2, 3]은 왼쪽으로 3칸 또는 오른쪽으로 4칸 순환 이동할 경우 완전히 정렬됩니다.

## 입력
### 인자 1 : rotated
number 타입을 요소로 갖는 배열
rotated[i]는 정수

### 인자 2 : target
number 타입의 정수

## 출력
number 타입을 리턴해야 합니다.

## 주의사항
rotated에 중복된 요소는 없습니다.
target이 없는 경우, -1을 리턴해야 합니다.

## 입출력 예시
```javascript
let output = rotatedArraySearch([4, 5, 6, 0, 1, 2, 3], 2);
console.log(output); // --> 5

output = rotatedArraySearch([4, 5, 6, 0, 1, 2, 3], 100);
console.log(output); // --> -1
```
## Advanced
단순히 처음부터 끝까지 찾아보는 방법(O(N)) 대신 다른 방법(O(logN))을 탐구해 보세요.

## 힌트
이진 탐색(binary search)을 약간 변형하여 해결합니다.

## 문제풀이
```javascript
const rotatedArraySearch = function (rotated, target) {
  // 시간 복잡도 O(logN)
  let left = 0, right = rotated.length - 1;

  while (left <= right) {
    let mid = Math.floor((left + right) / 2); // target을 찾는 기준점

    if (rotated[mid] === target) return mid;

    // 왼쪽 절반 정렬
    if (rotated[left] < rotated[mid]) {
      if (target < rotated[mid] && rotated[left] <= target) {
        right = mid - 1;
      } else {
        left = mid + 1;
      }
    } else {
      // 오른쪽 절반 정렬
      if (target <= rotated[right] && rotated[mid] < target) {
        left = mid + 1;
      } else {
        right = mid - 1;
      }
    }
  }
  return -1;
}

// 이진 탐색 => 배열 rotated의 중앙을 잡고 좌우를 탐색
// 이진 탐색을 위해 절반으로 나눠서 코딩하자

// 1. rotated 된 기준점(mid)을 찾는다.
// 2. 왼쪽과 오른쪽으로 정렬된 부분으로 나뉘어 탐색을 시작한다.
// 3. arr[mid]의 값이 왼쪽정렬(시작점 left) 값보다 크면 왼쪽 정렬 탐색을 시작한다. (왼쪽 절반이 정렬되어 있는 상태)
//  3-1.왼쪽정렬(left)부터 기준점 사이에 target이 포함하면 right = mid - 1
//  3-2.위 경우가 아니면, left = mid + 1
// 4. arr[mid]의 값이 왼쪽정렬(left) 값보다 작으면 오른쪽 정렬 탐색을 시작한다. (오른쪽 절반이 정렬되어 있는 상태)
//  4-1.기준점부터 오른쪽정렬(끝점 right) 사이에 target이 포함된다면 left = mid + 1
//  4-2.위 경우가 아니면, right = mid - 1
// 5. while 의 조건에 도달할 때까지 left와 right값이 변화함에 따라 mid(기준점)이 바뀌며 범위를 좁혀나간다.
// 6. arr[mid] 와 target 이 동일하면 인덱스 값인 mid 를 반환한다.
// 7. 그렇지 않을 경우, target이 존재하지 않으므로 -1 을 반환한다.

  // 시간 복잡도 O(n)
//   for (let i = 0; i < rotated.length; i++) {
//     if (rotated[i] === target) {
//       return i;
//     }
//   }
//   return -1;
// };
```

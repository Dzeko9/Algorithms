# 문제
정수를 요소로 갖는 배열을 입력받아 다음의 조건을 만족하는 LSCS*를 리턴해야 합니다.

* LSCS: 주어진 배열의 연속된 부분 배열*의 합을 구한다고 할 때, 이 중 가장 큰 값(Largest Sum of Contiguous Subarray)
* 연속된 부분 배열들: 배열 [1,2,3]의 연속 부분 배열은 [1], [1, 2], [1, 2, 3], [2], [2, 3], [3] 입니다.

## 입력
### 인자 1 : arr
* number 타입을 요소로 갖는 배열
* arr.length는 60,000 이하
* arr[i]는 -100,000 이상 100,000 이하의 정수

## 출력
* number 타입을 리턴해야 합니다.

## 주의사항
* 배열의 모든 요소가 음수인 경우도 있습니다.

## 입출력 예시
```javascript
let output = LSCS([1, 2, 3]);
console.log(output); // --> 6

output = LSCS([1, 2, 3, -4]);
console.log(output); // --> 6 ([1, 2, 3])

LSCS([1, 2, 3, -4, 5]);
console.log(output); // --> 7 ([1, 2, 3, -4, 5])

LSCS([10, -11, 11]);
console.log(output); // --> 11 ([11])
```

## Advanced
* LSCS를 계산하는 효율적인 알고리즘(O(N))이 존재합니다. 쉽지 않기 때문에 바로 레퍼런스 코드를 보고 이해하는 데 집중하시기 바랍니다.

## 문제풀이
```javascript
const LSCS = function(arr) {
  let max = Number.MIN_SAFE_INTEGER; // 음수가 나오기 전까지의 수를 더한 최대값
  let sum = 0; 

  // 시간 복잡도 O(n) => for문(1번)
  for (let i = 0; i < arr.length; i++) {
    sum += arr[i];
    if (sum > max) {
      max = sum;
    }
    // 연속된 요소의 합이 음수인 경우,
    // 음수가 나오면 합을 다시 0으로 만들어준 뒤 값을 계속 더해나간다.
    if (sum < 0) {
      sum = 0;
    }
  }
  return max;
};

// 계속 더하다가 음수가 더해지면 그 수는 음수가 더해지기 전까지의 값만이 최대값이다
// => 음수가 더해지면 그 수는 더이성 최대값이 아니고 더하기 전의 값이 최대값이다.
```

# 문제
오름차순 정렬된 정수의 배열(arr)과 정수(target)를 입력받아 target의 인덱스를 리턴해야 합니다.

## 입력
### 인자 1 : arr
number 타입을 요소로 갖는 배열
arr[i]는 정수

### 인자 2 : target
number 타입의 정수

## 출력
number 타입을 리턴해야 합니다.

## 주의사항
이진탐색 알고리즘(O(logN))을 사용해야 합니다.
단순한 배열 순회(O(N))로는 통과할 수 없는 테스트 케이스가 존재합니다.
target이 없는 경우, -1을 리턴해야 합니다.

## 입출력 예시
```javascript
let output = binarySearch([0, 1, 2, 3, 4, 5, 6], 2);
console.log(output); // --> 2

output = binarySearch([4, 5, 6, 9], 100);
console.log(output); // --> -1
```

## 문제풀이
```javascript
const binarySearch = function (arr, target) {
  let left = 0; // 왼쪽 인덱스 (작은쪽)
  let right = arr.length-1 // 오른쪽 인덱스 (큰쪽)

  while (left <= right){ // left가 right가 겹치지 않을때까지 반복
    // binarySearch는 가운데에서부터 작으면 가운데 기준으로 왼쪽 크면 오른쪽으로 잘라 향하기때문에 가운데를 지정 
    const middle = parseInt((left + right)/2) 

    if (arr[middle] < target){
      // 가운데가 타겟보다 작을경우는 오른쪽으로 향해야하기 때문에 왼쪽을 가운데 다음 인덱스로 지정
      left = middle+1;
    }else if (arr[middle] > target){
      // 가운데가 타겟보다 클경우는 왼쪽으로 향해야하기 때문에 오른쪽을 가운데 전 인덱스로 지정
      right = middle-1;
    }else if (arr[middle] === target){
      // 가운데에서 찾았을경우
      return middle;
    }
  }
  //여기까지 왔다는건 left와 right가 겹쳤다는것이고 arr에는 찾고자하는 타겟이 없음!
return -1

};
```

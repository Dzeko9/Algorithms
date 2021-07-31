# 문제
두 개의 배열(base, sample)을 입력받아 sample이 base의 부분집합인지 여부를 리턴해야 합니다.

## 입력

### 인자 1 : base
number 타입을 요소로 갖는 임의의 배열
base.length는 100 이하

### 인자 2 : sample
number 타입을 요소로 갖는 임의의 배열
sample.length는 100 이하

## 출력
boolean 타입을 리턴해야 합니다.

## 주의사항
base, sample 내에 중복되는 요소는 없다고 가정합니다.

## 입출력 예시
```javascript
let base = [1, 2, 3, 4, 5];
let sample = [1, 3];
let output = isSubsetOf(base, sample);
console.log(output); // --> true

sample = [6, 7];
output = isSubsetOf(base, sample);
console.log(output); // --> false

base = [10, 99, 123, 7];
sample = [11, 100, 99, 123];
output = isSubsetOf(base, sample);
console.log(output); // --> false
```

## Advanced
시간 복잡도를 개선하여, Advanced 테스트 케이스(base, sample의 길이가 70,000 이상)를 통과해 보세요.

## 문제풀이 
```javascript
const isSubsetOf = function (base, sample) {
  base = base.sort((a, b) => a - b);
  sample = sample.sort((a, b) => a - b);

  for (let i = 0; i < base.length; i++) {
    if (base[i] === sample[0]) {
      sample.shift();
    }
  }
  if (sample.length === 0) {
    return true;
  }
  return false;
};

// 최소한의 탐색으로 부분집합 여부를 찾아내야 한다 => 연산 횟수 줄이기

// base와 sample을 오름차순으로 정렬한다
// 정렬한 두 배열을 반복문으로 비교하여 같은 값이 있으면 sample에서 제거한다
// for loop가 끝나고 sample의 길이가 0이면 true 아니면 false (base의 부분집합)
```

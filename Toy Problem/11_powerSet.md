# 문제
하나의 집합을 의미하는 문자열을 입력받아 각 문자를 가지고 만들 수 있는 모든 부분집합을 리턴해야 합니다.

## 입력
### 인자 1 : str
string 타입의 공백이 없는 알파벳 소문자 문자열

## 출력
배열(arr)을 리턴해야 합니다.
arr[i]는 각 부분집합의 원소로 구성된 문자열

## 주의사항
arr[i]는 각 부분집합을 구성하는 원소를 연결한 문자열입니다.
arr[i]는 알파벳 순서로 정렬되어야 합니다.
집합은 중복된 원소를 허용하지 않습니다.
부분집합은 빈 문자열을 포함합니다.
arr은 사전식 순서(lexical order)로 정렬되어야 합니다.

## 입출력 예시
```javascript
let output1 = powerSet('abc');
console.log(output1); // ['', 'a', 'ab', 'abc', 'ac', 'b', 'bc', 'c']

let output2 = powerSet('jjump');
console.log(output2); // ['', 'j', 'jm', 'jmp', 'jmpu', 'jmu', 'jp', 'jpu', 'ju', 'm', 'mp', 'mpu', 'mu', 'p', 'pu', 'u']
```

## 문제풀이
```javascript
const powerSet = function (str) {
  // 문자열을 각각 분리하여 배열로 나누고 정렬
  const arr = str.split('').sort();

  // 중복제거
  const filtered = arr.filter((item, idx) => arr.indexOf(item) === idx);

  // DFS, 부분 집합 재귀 함수
  const subSets = [];
  function DFS(i, subset) {
    // base case (마지막 문자까지 검토한 경우)
    if (i === filtered.length) {
      subSets.push(subset);
      return;
    }

    // recursive case (모든 i 검토)
    // i번째 문자 포함x
    DFS(i + 1, subset);

    // i번째 문자 포함
    DFS(i + 1, subset + filtered[i])
  };

  DFS(0, ''); // 0부터 다시 시작(재귀함수 실행)
  return subSets.sort(); // 결과 알파벳 순서 정렬
};

// 멱집합 => 어떤 집합의 모든 부분 집합의 집합
// 비어있는 집합을 포함한 모든 부분집합(subset)의 모음

// 1. 중복단어 제외
// 2. 알파벳 순서 정렬 (사전식 순서)
// 3. 빈 문자열 포함

  //           a(o)                    b(o)                    c(o)
  //    a      b(o)   c(o)      a      b      c(o)      a      b      c
  //  a b c   a b c  a b c    a b c  a b c  a b c     a b c  a b c  a b c
  //  x x x   x x o  x x x    x x x  x x x  x x x     x x x  x x x  x x x
```

# 문제
세로 길이 2, 가로 길이 n인 2 x n 보드가 있습니다. 2 x 1 크기의 타일을 가지고 이 보드를 채우는 모든 경우의 수를 리턴해야 합니다.

## 입력
### 인자 1 : n
number 타입의 1 이상의 자연수

## 출력
number 타입을 리턴해야 합니다.

## 주의사항
타일을 가로, 세로 어느 방향으로 놓아도 상관없습니다. (입출력 예시 참고)

## 입출력 예시
```javascript
let output = tiling(2);
console.log(output); // --> 2

output = tiling(4);
console.log(output); // --> 5
/* 
2 x 4 보드에 타일을 놓는 방법은 5가지
각 타일을 a, b, c, d로 구분

2 | a b c d
1 | a b c d 
------------

2 | a a c c
1 | b b d d 
------------

2 | a b c c
1 | a b d d 
------------

2 | a a c d
1 | b b c d 
------------

2 | a b b d
1 | a c c d 
------------
*/
```

## Advanced
타일링 문제를 해결하는 효율적인 알고리즘(O(N))이 존재합니다. 반드시 직접 문제를 해결하시면서 입력의 크기에 따라 어떻게 달라지는지 혹은 어떻게 반복되는지 관찰하시기 바랍니다.

## 문제풀이
```javascript
// 인덱스 관리를 위한 dummyData
const memo = [1, 2, 3]

let tiling = function (n) {
  // 효율적인 알고리즘을 위해 미리 조건 분기
  if(n <= 2) return n;
  // 3부터는 피보나치 수열을 이룬다
  if (memo[n] === undefined) {
    memo[n] = tiling(n - 1) + tiling(n - 2);
  }
  return memo[n];
};

// 타일을 가로로 놓는법 => =
// 타일을 세로로 놓는법 => ||
// 2 x 4 타일을 채우는 방법은 2 x 3 타일 + 2 x 2 타일 
// => 결국 2 x n = 2 x (n-1) + 2 x (n-2)
// 모든 경우의 수를 구할때까지 재귀
// 재귀로만 접근할 경우 시간 복잡도가 O(2^n)
// memoization으로 접근해서 시간복잡도를 줄여준다.

// | | | |
// = =
// | | =
// = | |
// | = | 

// 1 --> 1
// 2 --> 2
// 3 --> 3
// 4 --> 5
// 5 --> 8
// 6 --> 13

// 재귀 보조 함수
//   const aux = (size) => {
//     // 이미 해결한 문제는 풀지 않는다.
//     if (memo[size] !== undefined) return memo[size];
//     if (size <= 2) return memo[n];
//     memo[size] = aux(size - 1) + aux(size - 2);
//     return memo[size];
//   };
//   return aux(n);
// };
```

# 문제
2차원 N x N 배열을 시계 방향으로 90도 회전시킨 배열을 리턴해야 합니다.

## 입력
### 인자 1 : matrix
가로 길이(matrix[i].length)와 세로 길이(matrix.length)가 모두 N인 2차원 배열
matrix[i][j]는 number 타입

## 출력
2차원 배열을 리턴해야 합니다.

## 입출력 예시
```javascript
const matrix = [
  [1, 2, 3, 4],
  [5, 6, 7, 8],
  [9, 10, 11, 12],
  [13, 14, 15, 16],
];
console.log(matrix[0][0]); // --> 1
console.log(matrix[3][2]); // --> 15

const rotatedMatrix = rotateMatrix(matrix);
console.log(rotatedMatrix[0][0]); // --> 13
console.log(rotatedMatrix[3][2]); // --> 8
```

## 힌트
* 컴퓨터 과학에서 행렬은 '행'의 길이인 m과 '열'의 길이인 n의 곱으로 표현됩니다. m X n 행렬은 아래와 같이 2차원 배열로 구현할 수 있습니다. (행렬의 요소를 전부 initVal로 초기화)
```javascript
const matrix = [];
for(let row = 0; row < m; row++>) {
  matrix.push(Array(n).fill(initVal))
}
```
이때 matrix[i][j]는 '행(세로축)을 기준으로 i만큼 아래에 있고 열(가로축)을 기준으로 j만큼 옆에 있다.`를 뜻합니다. 이 방식은 기하학에서 좌표 평면 위의 한 점을 나타낼 때 (x, y), 즉 가로축을 먼저 표기하고 세로축을 다음에 표기하는 방식과는 다릅니다. 그래프를 인접행렬로 구현할 때, 이 점을 주의하셔야 합니다.

## Advanced
세로와 가로의 길이가 각각 M, N인 2차원 M X N 배열을 시계방향으로 90도씩 K번 회전시킨 배열을 리턴해 보세요. 회전수가 두 번째 입력으로 주어집니다.

## 문제풀이
```javascript
const rotateMatrix = function (matrix, k=1) { // k 값을 받아와서 k번 실행
  if(matrix.length === 0) return matrix;
  
  for(let i = 0; i < k; i++){ // k번 실시(advanced)
    matrix = rotate(matrix);
  }

  return matrix
};

const rotate = (matrix) => {
  let result = [];

  for(let row = 0; row < matrix[0].length; row++) {
    let array = []
    for(let col = matrix.length-1; col >= 0; col--){
      array.push(matrix[col][row])
    } // [13, 9, 5, 1]의 배열 생성 -> [14, 10, 6, 2]의 배열 생성
    result.push(array)
  }

  return result
};

// 배열의 위치를 재정의 해주는 문제..?
// 행렬의 길이가 N이라고 할 때, [y, x]은 [x, N - 1 - y]의 좌표로 옮겨지는 규칙
// before 배열의 x값 인덱스는 after 배열의 y값 인덱스로 바뀌고,
// before 배열의 y값 인덱스는 after 배열의 N - i - 1 인덱스로 바뀐다.

//   const N = matrix.length;
//   const M = matrix[0] && matrix[0].length;
//   let result = [];

//   for (let row = 0; row < M; row++) {
//     result[row] = [];
//     for (let col = 0; col < N; col++) {
//       result[row][col] = matrix[N - col - 1][row];
//     }
//   }

//   return result;
// };
```

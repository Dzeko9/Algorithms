# 문제
스도쿠는 숫자 퍼즐로, 가로 9칸, 세로 9칸으로 이루어져 있는 표에 1부터 9까지의 숫자를 채워 넣는 퍼즐입니다. 퍼즐을 푸는 방법은 아홉 가로줄, 세로줄, 3X3 칸에 1에서 9까지의 숫자를 중복되지 않게 한 번씩만 넣으면 됩니다. 일부 칸이 비어있는 상태인 스도쿠 보드를 입력받아 스도쿠 퍼즐이 완성된 보드를 리턴해야 합니다.

## 입력
### 인자 1 : board
가로 길이(board[i].length)와 세로 길이(board.length)가 모두 9인 2차원 배열
matrix[i][j]는 1 이상 9 이하의 자연수

## 출력
가로와 세로의 길이가 모두 9인 2차원 배열을 리턴해야 합니다.

## 주의사항
입력으로 주어지는 board를 직접 수정해도 상관없습니다.
입력으로 주어지는 board 가지고 완성시킬 수 있는 보드는 유일(unique)합니다.
숫자가 입력되지 않은 칸은 편의상 0이 입력되어 있습니다.

## 입출력 예시
```javascript
let board = [
  [0, 3, 0, 2, 6, 0, 7, 0, 1],
  [6, 8, 0, 0, 7, 0, 0, 9, 0],
  [1, 9, 0, 0, 0, 4, 5, 0, 0],
  [8, 2, 0, 1, 0, 0, 0, 4, 0],
  [0, 0, 4, 6, 0, 2, 9, 0, 0],
  [0, 5, 0, 0, 0, 3, 0, 2, 8],
  [0, 0, 9, 3, 0, 0, 0, 7, 4],
  [0, 4, 0, 0, 5, 0, 0, 3, 6],
  [7, 0, 3, 0, 1, 8, 0, 0, 0],
];
let output = sudoku(board);
console.log(output); // -->
/* 
[
  [4, 3, 5, 2, 6, 9, 7, 8, 1],
  [6, 8, 2, 5, 7, 1, 4, 9, 3],
  [1, 9, 7, 8, 3, 4, 5, 6, 2],
  [8, 2, 6, 1, 9, 5, 3, 4, 7],
  [3, 7, 4, 6, 8, 2, 9, 1, 5],
  [9, 5, 1, 7, 4, 3, 6, 2, 8],
  [5, 1, 9, 3, 2, 6, 8, 7, 4],
  [2, 4, 8, 9, 5, 7, 1, 3, 6],
  [7, 6, 3, 4, 1, 8, 2, 5, 9],
];
 */
 ```
 
 ## 문제풀이
 ```javascript
 const sudoku = function (board) {
  // N = board.length = 9 
  // 1 ~ 9 까지 3 X 3 배열로 나눔
  const N = board.length;
  const boxes = [
    [0, 0, 0, 1, 1, 1, 2, 2, 2],
    [0, 0, 0, 1, 1, 1, 2, 2, 2],
    [0, 0, 0, 1, 1, 1, 2, 2, 2],
    [3, 3, 3, 4, 4, 4, 5, 5, 5],
    [3, 3, 3, 4, 4, 4, 5, 5, 5],
    [3, 3, 3, 4, 4, 4, 5, 5, 5],
    [6, 6, 6, 7, 7, 7, 8, 8, 8],
    [6, 6, 6, 7, 7, 7, 8, 8, 8],
    [6, 6, 6, 7, 7, 7, 8, 8, 8],
  ];
  // row , col 위치(가로, 세로)
  const getBoxNum = (row, col) => boxes[row][col];
  const blanks = []; // 비어있는 (값이 0인) 칸의 위치값이 저장
  const rowUsed = []; // n번째 행에 m이라는 숫자가 존재하는 지의 여부가 true, false로 저장
  const colUsed = []; // i번째 행에 m이라는 숫자가 존재하는 지의 여부가 true, false로 저장
  const boxUsed = []; // j번째 박스에 m이라는 숫자가 존재하는 지의 여부가 true, false로 저장

  for (let row = 0; row < N; row++) { 
    rowUsed.push(Array(N + 1).fill(false)); // 모든 값을 false로 초기화
    colUsed.push(Array(N + 1).fill(false));
    boxUsed.push(Array(N + 1).fill(false));
  } // fill() 메서드는 배열의 시작 인덱스부터 끝 인덱스의 이전까지 정적인 값 하나로 채운다.

  for (let row = 0; row < N; row++) { // 행과 열을 board의 길이만큼 순회
    for (let col = 0; col < N; col++) {
      if (board[row][col] === 0) { // 2차원 배열을 순회하면서 특정 위치의 값이 0이라면,
        blanks.push([row, col]); // 해당 위치(행,열)를 blanks 배열에 추가
      } else { // board[행,열]이 값을 가지고 있다면,
        const num = board[row][col]; // 해당 값을 가져오고
        const box = getBoxNum(row, col); // box 번호도 가져오고
        rowUsed[row][num] = true; // 해당 행에 해당 값이 있다는 것을 표시해주고,
        colUsed[col][num] = true; // 해당 열에 해당 값이 있다는 것을 표시해주고,
        boxUsed[box][num] = true; // 해당 box에 해당 값이 있다는 것을 표시
      }
    }
  }

  // row번째 행, col번째 열, box에 num을 입력이 가능한 지 확인
  const isValid = (row, col, num) => {
    const box = getBoxNum(row, col); // box 값을 가져옴
    return (
      rowUsed[row][num] === false && // 해당 행에 num이 없으면, 즉 해당 행에 num을 입력할 수 있고
      colUsed[col][num] === false && // 해당 열에 num을 입력할 수 있고
      boxUsed[box][num] === false // 해당 box에 num을 입력할 수 있으면, num은 입력이 가능한 숫자
      // 셋 중 하나라도 false라면 false가 리턴
    );
  };

  // board에 num을 입력해주고, 해당 행,열,box의 num에 대한 값이 true면 false로, false면 true로 바꿔준다.
  // 왜냐하면, 입력이 가능한 숫자인 줄 알았다가 나중에 확인해보니 아닌 경우도 있기 때문에..
  // 그렇기 때문에 toggle 형식으로 구현
  const toggleNum = (row, col, num) => {
    const box = getBoxNum(row, col);
    board[row][col] = num; // 실제적으로 board에 값을 입력하는 부분
    rowUsed[row][num] = !rowUsed[row][num];
    colUsed[col][num] = !colUsed[col][num];
    boxUsed[box][num] = !boxUsed[box][num];
  };

  // 재귀적으로 호출이 될 보조함수
  const aux = (idx, blanks, board) => {
    if (idx === blanks.length) { // blank 배열의 모든 요소를 탐색했을 때, 즉 모든 탐색이 끝났을 때 true 리턴
      return true;
    }

    const [row, col] = blanks[idx]; // 비어 있는(0으로 채워진) 자리의 위치값을 구조분해할당을 통해 row와 col 변수에 할당
    for (let num = 1; num <= 9; num++) { // 1~9의 숫자를 순회하며 비어 있는 자리에 num을 입력할 수 있는 지 확인
      if (isValid(row, col, num) === true) { // num을 해당 행,열,box에 입력이 가능하다면
        toggleNum(row, col, num); // toggleNum 함수를 통해 board에 num을 입력
        if (aux(idx + 1, blanks, board) === true) { // 비어 있는 칸을 조회하기 위한 재귀적 호출
          return true; // true 리턴 시(blanks의 모든 요소를 탐색 완료했을 시) true를 리턴
        }
        toggleNum(row, col, num); // // 재귀함수가 false를 리턴했을 시, true였던 값을 모두 false 처리해주고 그 다음 숫자 입력
      }
    }
    return false; // 1~9의 숫자가 모두 입력이 불가능 할 시에, false 리턴
    // 그렇다면 이전으로 돌아가 toggleNum 함수를 호출하여 true였던 값을 false로 바꿔주고, 그 다음 숫자를 선택해 탐색을 진행
  };

  aux(0, blanks, board); // 최초 함수를 실행하는 부분 (인덱스 0, blanks, board를 인자로 전달)
  return board; // 최종 스도쿠 판 리턴
};
// 각각의 가로줄과 세로줄에는 1부터 9까지의 숫자가 한 번씩만 나타나야 한다.
// 1. 가로를 체크
// 2. 세로를 체크
// 3. 3X3을 체크
 ```

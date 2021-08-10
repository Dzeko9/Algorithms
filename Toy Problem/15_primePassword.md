# 문제
다음의 조건을 만족하면서 현재의 비밀번호('curPwd')를 새 비밀번호(newPwd)로 변경하는 데 필요한 최소 동작의 수를 리턴해야 합니다.

* 한 번에 한 개의 숫자만 변경가능하다.
* 4자리의 소수(prime)인 비밀번호로만 변경가능하다.

정리하면, 비밀번호가 계속 소수를 유지하도록 숫자 한 개씩을 바꿔갈 때 현재 비밀번호에서 새 비밀번호로 바꾸는 데 최소 몇 개의 숫자를 변경해야 하는지를 리턴해야 합니다.

## 입력
### 인자 1 : curPwd
number 타입의 1,000 이상 9,999 이하의 자연수

### 인자 2 : newPwd
number 타입의 1,000 이상 9,999 이하의 자연수

## 출력
number 타입을 리턴해야 합니다.

## 주의사항
4자리인 소수는 1,000 이상의 소수를 말합니다.(0011, 0997 등은 제외)

## 입출력 예시
```javascript
let output = primePassword(1033, 1033);
console.log(output); // --> 0

output = primePassword(3733, 8779);
console.log(output); // --> 3 (3733 -> 3739 -> 3779 -> 8779)
```

## 문제풀이
```javascript
// const primePassword = (curPwd, newPwd) => {
//   // base case
//   if (curPwd === newPwd) {
//     return 0;
//   }
//   let count = 0;
//   let splitCurPwd = String(curPwd).split('');
//   let splitNewPwd = String(newPwd).split('');
//   while(curPwd !== newPwd) {
//     for(let i = 3; i >= 0; i --) { // 1의자리부터 각 자리수 확인
//       for(let j = 0 ; j < 9; j ++) {
//         splitCurPwd[i] = j;
//         if(splitCurPwd[i] === splitNewPwd[i]) {
//           break;
//         }
//         if(isPrime(Number(splitCurPwd.join('')))) {
//           count ++;
//         }
//       }
//     }
//   }
//   return count;
// }

  // 소수 판별 함수
  const isPrime = (n) => {
    if (n % 2 === 0) return false;
    let sqrt = parseInt(Math.sqrt(n));
    for (let divider = 3; divider <= sqrt; divider += 2) {
      if (n % divider === 0) {
        return false;
      }
    }
  return true;
};
  // 각 자리 수들을 배열로 변환하는 함수
  const splitNum = (n) => {
    const digits = num.toString().split('');
    return digits.map((digits) => Number(digits));
  }

  // 길이 4의 배열을 받아서, 4자리 수로 변환하는 함수
  const joingDigits = (digits) => Number(digits.join(''));

  // base case
  const primePassword = (curPwd, newPwd) => {
    if (curPwd === newPwd) return 0;

  // BFS (queue 사용)
  let front = 0;
  let rear = 0;
  const queue = [];

  const isEmpty = (q) => front === rear;
  const enQueue = (q, item) => {
    queue.push(item);
    rear++;
  }

  const deQueue = (q) => {
    return queue[front];
  }
}
```

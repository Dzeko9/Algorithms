# 문제
문자열을 입력받아 문자열 내의 모든 괄호의 짝이 맞는지 여부를 리턴해야 합니다.

* 다음 단계에 맞춰 함수를 작성해 보세요
  1. 괄호의 종류를 단 한가지로 한정합니다.
  2. 괄호의 종류를 늘려 모든 종류의 괄호에도 작동하도록 합니다.
  3. 괄호를 제외한 문자열이 포함된 경우에도 작동하도록 합니다.

## 입력
### 인자 1 : str
string 타입의 괄호가 포함된 문자열

## 출력
boolean 타입을 리턴해야 합니다.

## 주의사항
괄호의 종류는 (, )만 고려합니다.
괄호는 먼저 열리고((), 열린만큼만 닫혀야()) 합니다.
빈 문자열을 입력받은 경우, true를 리턴해야 합니다.

## 입출력 예시
```javascript
let output = balancedBrackets('(');
console.log(output); // // -> false

output = balancedBrackets('()');
console.log(output); // --> true
```

## Advanced
모든 종류의 괄호((, ), {, }, [, ])가 포함된 문자열을 입력빋아 모든 괄호의 짝이 맞는지 여부를 리턴해 보세요.
```javascript
let output = balancedBrackets('[](){}');
console.log(output); // --> true

output = balancedBrackets('[({})]');
console.log(output); // --> true

let output3 = balancedBrackets('[(]{)}');
console.log(output); // --> false
```

## 문제풀이
```javascript
const balancedBrackets = function (str) {
  const brakets = '(){}[]';
  const stack = [];

  for (let key of str) {
    let idx = brakets.indexOf(key);
    //  괄호 인덱스 구하기
    if (idx % 2 === 0) { // 닫히는 괄호 인덱스에 넣어주기
      stack.push(idx + 1);
    } else { // 홀수 인덱스일 때
      if (stack.pop() !== idx) { // stack에서 빼주는데, 값이 같지 않으면 괄호가 제대로 안 닫힌 경우
        return false;
      }
    }
  }
  return stack.length > 0 ? false : true;
};

//   // 배열 형태
//   const arr = str.split("");
//   const stack = [];
//   for (let el of arr) {
//     // opener
//     if (el === "{" || el === "[" || el === "(") {
//       stack.push(el);
//       // closer
//     } else { 
//       if (stack.length === 0) {
//         return false;
//       }
//       if (el === "}" && stack[stack.length - 1] === "{") { 
//         //  {} 쌍이 맞는지 확인
//         stack.pop();
//       } else if (el === "]" && stack[stack.length - 1] === "[") { 
//         //  [] 쌍이 맞는지 확인
//         stack.pop();
//       } else if (el === ")" && stack[stack.length - 1] === "(") {
//         //  () 쌍이 맞는지 확인
//         stack.pop();
//       } else if(el === "}" || el === "]" || el === ")") { 
//         //  쌍이 안 맞는 경우엔 stack에 넣는다
//         stack.push(el);
//       }
//     }
//   }
//   return stack.length > 0 ? false : true;
// };

//   const stack = [];
//   const opener = {
//     '{': '}',
//     '[': ']',
//     '(': ')',
//   };
//   const closer = '}])';

//   for (let i = 0; i < str.length; i++) {
//     if (str[i] in opener) {
//       stack.push(str[i]);
//     } else if (closer.includes(str[i])) {
//       const top = stack.pop();
//       const pair = opener[top];
//       if (pair !== str[i]) {
//         return false;
//       }
//     }
//   }

//   return stack.length === 0;
// };
```

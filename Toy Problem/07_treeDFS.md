# 문제
임의의 tree를 구성하는 노드 중 하나의 Node 객체를 입력받아, 해당 노드를 시작으로 깊이 우선 탐색(DFS, Depth First Search)을 합니다. 이 때, 탐색되는 순서대로 노드의 값이 저장된 배열을 리턴해야 합니다.

## 입력
### 인자 1 : node
'value', 'children' 속성을 갖는 객체 (Node)
'node.value'는 number 타입
'node.children'은 Node를 요소로 갖는 배열

## 출력
배열을 리턴해야 합니다.

## 주의사항
생성자 함수(Node)와 메소드(addChild)는 변경하지 않아야 합니다.

## 입출력 예시
```javascript
let root = new Node(1);
let rootChild1 = root.addChild(new Node(2));
let rootChild2 = root.addChild(new Node(3));
let leaf1 = rootChild1.addChild(new Node(4));
let leaf2 = rootChild1.addChild(new Node(5));
let output = dfs(root);
console.log(output); // --> [1, 2, 4, 5, 3]

leaf1.addChild(new Node(6));
rootChild2.addChild(new Node(7));
output = dfs(root);
console.log(output); // --> [1, 2, 4, 6, 5, 3, 7]
```

## 문제풀이
```javascript
let dfs = function (node) {
  const result = [];
  let rec = (node) => {
    if (node.value) { // 만약 children이 있으면?
      result.push(node.value); // 배열에 value를 푸쉬
      for (let i = 0; i < node.children.length; i++) {
        rec(node.children[i]); // 내부의 children 순서대로 재귀
      }
    } else {
      result.push(node.value);
    }
  }
  rec(node);
  return result;
};

// 이 아래 코드는 변경하지 않아도 됩니다. 자유롭게 참고하세요.
let Node = function (value) {
  this.value = value;
  this.children = [];
};

// 위 Node 객체로 구성되는 트리는 매우 단순한 형태의 트리입니다.
// membership check(중복 확인)를 따로 하지 않습니다.
Node.prototype.addChild = function (child) {
  this.children.push(child);
  return child;
};


// 재귀 혹은 스택을 사용하여 구현하는 특징 => DFS
// 1. 탐색 시작 노드를 스택에 삽입하고 방문 처리를 한다 (방문기준 : (보통) 번호가 낮은 인접 노드부터 시작)
// 2. 스택의 최상단 노드에 방문하지 않은 인접 노드가 없으면, 스택에서 최상단 노드를 꺼낸다
// 3. 더이상 2의 과정을 수행할 수 없을 때까지 반복한다.


  // let values = [node.value];

  // node.children.forEach((n) => {
  //   values = values.concat(dfs(n));
  // });

  // return values;
  
// 부모노드 value를 배열에 담아 => [node.value] => 변수에 저장
// 만약 children이 있으면? 각각의 children 값을 배열에 담아 
// 부모노드 value가 있는 배열의 뒤에 추가 => 이렇게 자식 노드 끝까지 탐색
```

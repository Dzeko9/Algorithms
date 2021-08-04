# 문제
임의의 tree를 구성하는 노드 중 하나의 Node 객체를 입력받아, 해당 노드를 시작으로 너비 우선 탐색(BFS, Breadth First Search)을 합니다. 이 때, 탐색되는 순서대로 노드의 값이 저장된 배열을 리턴해야 합니다.

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
let output = bfs(root);
console.log(output); // --> [1, 2, 3, 4, 5]

leaf1.addChild(new Node(6));
rootChild2.addChild(new Node(7));
output = bfs(root);
console.log(output); // --> [1, 2, 3, 4, 5, 7, 6]
```

## 문제풀이
```javascript
let bfs = function (node) {
  let result = [];
  let queue = [node] // 조회할 노드들을 순차적으로 넣음

  while(queue.length > 0) { // 조회할 노드가 남아있으면 => 모두 빠져나갈 때까지
    let pick = queue.shift(); // 노드를 하나 지정
    result.push(pick.value); // 대상 노드의 값을 결과에 저장
    
    for (let i = 0; i < pick.children.length; i++) {
      queue.push(pick.children[i]) // 자식의 노드들을 순차적으로 queue에 쌓아준다.
    }
  }
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

// 모든 노드를 순서대로 조회하기 때문에 넓이 우선 탐색이 구현
// Queue를 사용하여 트리의 노드들을 레벨별로 탐색
// for loop를 통해 queue 안에 있는 노드들을 하나씩 탐색하고 자식이 있다면 queue에 넣음
// queue 안에 아무 것도 나지 않았다면 다 탐색한 것이기에 그때 값을 담은 배열을 리턴
```

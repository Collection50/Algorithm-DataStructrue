# Tortoise & Hare

#알고리즘#연결리스트#토끼와거북이

## 개념
- 링크드 리스트의 Cycle 여부 확인
- 거북이와 토끼가 경주를 하는 것처럼, 토끼 == 2개 노드씩 이동하고 거북이 == 1개씩 이동
- 거북이와 토끼 만남 == Cycle 존재, 토끼가 먼저 `null`에 도달 == Cycle 없음

## 특징
1. 사이클이 존재할 때, 사이클의 **시작점**과 **길이**를 **시간 복잡도 O(N)**으로 탐색 가능
2. 링크드 리스트의 **투 포인터**

## 구현 메서드
- `hasCycle(linkedList)`: 링크드 리스트 Cycle 존재 여부(`true`, `false`), `tort`, `hare` 반환
- `getCycleStartNode(value)`: Cycle 존재 시 Cycle 시작 노드 반환
- `getCycleLength()`: Cycle 존재 시 Cycle의 길이 반환

## Implemention
```js
const hasCycle = (linkedList) => {
  let tort = linkedList;
  let hare = linkedList;
  while (hare && hare.next) {
    tort = tort.next;
    hare = hare.next.next;
    if (hare === tort) return [tort, hare, true];
  }
  return [tort, hare, false];
};

const getCycleStartNode = function (linkedList) {
  let [tort, hare, isCycle] = hasCycle(linkedList);
  if (!isCycle) return null;

  tort = linkedList;
  while (hare !== tort) {
    tort = tort.next;
    hare = hare.next;
  }
  return hare;
};

const getCycleLength = function (linkedList) {
  const cycleStartNode = getCycleStartNode(linkedList);
  const cycleEndNode = cycleStartNode.next;
  if (!cycleStartNode) return null;

  let count = 1;
  while (cycleStartNode !== cycleEndNode) {
    cycleStartNode = cycleStartNode.next;
    count++;
  }
  return count;
};
```

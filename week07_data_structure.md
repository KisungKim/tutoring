---
layout: default
title: "Binary Search Tree 기본개념, 삽입, 삭제 이해하기"
---

> ## Binary Search Tree 탐색, 삽입, 삭제 이해하기

## Binary Search Tree 기본개념

### 포화 이진 트리와 완전 이진 트리

> 포화 이진 트리는 모든 레벨(트리의 높이)의 노드가 가득 차있는 상태를 의미한다
>
> ex> 높이가 3인 트리라면, 총 6개의 노드(1+2+3)가 존재해야 한다
>
> 완전 이진 트리는 마지막 인덱스의 노드까지 빈 자리가 없는 이진트리를 의미한다.

### 트리를 배열로 구현하는 경우 다음을 기억하면 쉽다

> index의 시작은 0이 아닌 1로 하는 것이 덜 헷갈린다.(트리의 head index를 0이 아닌 1로) 
>
> 부모의 Left Child는 부모 index * 2 의 index를 가진다
>
> 부모의 Right Child는 부모 index * 2 + 1 의 index를 가진다
>
> ex > 1의 Left Child는 2, 2의 Left Child는 4
>
> ex > 1의 Right Child는 3, 2의 Right Child는 5
>
>
> 배열로 구현하는 경우 
>
> 만약 현재 index보다 더 큰 size의 index를 탐색해야 하는 경우, 배열을 어느 크기까지 증가시키는지에는 따로 정해진 바가 없다.
>
> 다만 트리의 높이를 1씩 증가시키는 것이 코드로 짜기 편리하다.
>
> ex > 높이가 3인 트리에서(1 23 456) 4인 트리로 증가(1 23 456 **7890(추가)**)

## Binary Search Tree 삽입

```python
class Node:
    def __init__(self):
        self.key = None
        self.left = None
        self.right = None
        

def insertBST(bst, x):
    ptr = bst                # 이진 탐색 트리의 head를 얻어옵니다.
    parent = None            # 앞으로 탐색할 노드의 부모자리를 저장합니다
    while ptr is not None:   # 이진 탐색 트리가 None을 만나기 전까지 반복합니다
        if x == ptr.key:     # 이진 탐색 트리에서는 중복되는 key를 허용하지 않습니다.
            return
        parent = ptr         # 현재 노드를 부모의 노드에 저장합니다
        if x < ptr.key:
            ptr = ptr.left   # 현재 노드를 현재 노드의 자식 노드로 이동합니다
        else:
            ptr = ptr.right
    
    newNode = Node()         # 새로운 노드를 만들어 줍니다
    newNode.key = x
    newNode.left = None
    newNode.right = None
    
    if bst is None:          # 만약 기존의 이진 탐색 트리가 없다면 새로운 노드를 이진탐색트리의 head로 설정해 줍니다
        bst = newNode
    elif x < parent.key:     # 부모의 오른쪽 자식인지, 왼쪽 자식인지에 따라 다음의 조건문을 따릅니다.
        parent.left = newNode
    else:
        parent.right = newNode
        
```

## Binary Search Tree 삭제

```python
```

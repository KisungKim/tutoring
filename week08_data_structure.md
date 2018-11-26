---
layout: default
title: "스택을 활용하여 BST의 데이터들 오름차순으로 출력하기"
---

> ## 스택을 활용하여 BST의 데이터들 오름차순으로 출력하기

### 포화 이진 트리와 완전 이진 트리

> 해당 알고리즘이 구현되는 원리는 다음과 같습니다.
>
>
> 전제조건 > left child는 parent node의 작은 값, right child는 parent node보다 항상 큰 값을 보인다.
>
>
>
> 순서 > 
> 1) 가장 작은 값을 탐색하며 내려갑니다. 이때, 해당 node에 left node가 존재한다면, 해당 node를 스택에 저장하며 1)을 반복합니다.
>
>
> 2) 해당 node에 left node가 존재하지 않는다면 현재 node는 앞으로의 탐색이 이루어져도 가장 작은 값이라고 할 수 있습니다. 따라서 스택에 넣지 않고 해당 노드의 데이터 값을 print합니다
>
>
> 3) 만약 해당 node에 right child가 있다면 이는 두 번째로 작은 값을 의미하므로 현재 노드를 right child의 노드로 대체하고 다시 1)을 반복합니다
>
>
> 4) 만약 해당 node에 right child가 없다면 스택에 마지막으로 저장된  node가 두 번째로 작은 값을 의미하므로 현재 노드를 스택에서 pop한 노드로 대체해 2)부터 반복합니다

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.Llink = None
        self.Rlink = None


class BST:
    def __init__(self):
        self.root = None

    def Tprint(self):
        stacknode = []
        self.cp = self.root
        self.left_not_visited = True

        while True:
            if self.cp.Llink is not None and self.left_not_visited is True:
                stacknode.append(self.cp)
                self.cp = self.cp.Llink
                continue

            print(self.cp.data, end=" ")

            if self.cp.Rlink is not None:
                self.cp = self.cp.Rlink
                self.left_not_visited = True
            else:
                if len(stacknode) != 0:
                    self.cp = stacknode.pop()
                    self.left_not_visited = False
                else:
                    break


    def insert(self, node):
        newnode = Node(node)
        if self.root == None:
            self.root = newnode

        else:
            self.CP = self.root
            self.PP = None
            while self.CP != None:
                if self.CP.data == newnode.data:
                    print("중복된 데이터가 있습니다.")
                    break

                elif self.CP.data > newnode.data:
                    self.PP = self.CP
                    self.CP = self.CP.Llink

                else:
                    self.PP = self.CP
                    self.CP = self.CP.Rlink

            if self.PP.data < newnode.data:
                self.PP.Rlink = newnode
            else:
                self.PP.Llink = newnode


B1 = BST()
B1.insert(5)
B1.insert(6)
B1.insert(3)
B1.insert(2)
B1.insert(9)
B1.insert(7)

B1.insert(4)


B1.Tprint()
```

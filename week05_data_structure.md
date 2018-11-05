---
layout: default
title: "Stack을 각각 리스트와 배열로 구현하기"
---

> ## Stack을 각각 리스트와 배열로 구현하기
> 파이썬으로 구현한 코드입니다.
>
> 같은 스택도 이전에 배웠던 리스트와 배열로 어떻게 구현을 하느냐에 따라 내부의 구동방식이 달라지게 됩니다. 
> 배열의 경우 사이즈가 항상 일정한 스택을 만들 수도 있지만, 더 큰 사이즈의 배열을 만들고 거기에 이전 배열을 복사하여 
> 새로운 배열을 만들어 동적으로 배열의 크기가 변화하는 스택을 만들 수 있습니다. 
> 리스트의 경우 노드 클래스를 활용할 수 있습니다. 

```python
class ArrayStack:
    def __init__(self):
        self.stack_list = []
        self.size = 0

    def push(self, input_item):
        self.size += 1
        temp_size = self.size
        if temp_size > len(self.stack_list):
            temp_list = [None] * temp_size
            temp_list[:temp_size-1] = self.stack_list
            temp_list[temp_size-1] = input_item
            self.stack_list = temp_list
        else:
            self.stack_list[temp_size-1] = input_item

    def pop(self):
        if self.size == 0:
            return
        self.size -= 1
        temp_size = self.size
        return self.stack_list[temp_size]


class Node:
    def __init__(self, data):
        self.next = None
        self.data = data


class ListStack:
    def __init__(self):
        self.size = 0
        self.item = None

    def push(self, input_item):
        if self.size == 0:
            self.item = Node(input_item)
        else:
            temp_node = Node(input_item)
            temp_node.next = self.item
            self.item = temp_node
        self.size += 1

    def pop(self):
        if self.size == 0:
            return
        if self.size == 1:
            temp_node = self.item
            self.item = None
            self.size -= 1
            return temp_node.data

        temp_node = self.item
        self.item = temp_node.next
        self.size -= 1
        return temp_node.data

    def print_list(self):
        temp_node = self.item
        while temp_node is not None:
            print(temp_node.data, "->", end=" ")
            temp_node = temp_node.next
        print()


stack1 = ArrayStack()
stack2 = ListStack()

print("=== Array stack ===")
stack1.push(1)
stack1.push(2)
stack1.push(3)
print(stack1.pop())
print(stack1.pop())
print(stack1.pop())
stack1.push(4)
stack1.push(5)
stack1.push(6)
print(stack1.pop())
print(stack1.pop())
print(stack1.pop())
print("===================")

print("=== List stack ===")
stack2.push(1)
stack2.push(2)
stack2.push(3)
stack2.print_list()
print(stack2.pop())
print(stack2.pop())
print(stack2.pop())
print("==================")
```

```
출력예시
-------
=== Array stack ===
3
2
1
6
5
4
===================
=== List stack ===
3 -> 2 -> 1 -> 
3
2
1
==================

```

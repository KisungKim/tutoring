---
layout: default
title: "Queue를 노드를 활용한 리스트로 구현하기"
---

> ## Queue를 노드를 활용한 리스트로 구현하기
> 파이썬으로 구현한 코드입니다.
>
> 큐 또한 스택과 마찬가지로 fixed된 사이즈가 아닌, 동적으로 크기를 증가시킬 수 있습니다
>
> 원형큐에서 중요한 점은 first가 전체 크기 중 하나를 항상 차지한다는 점입니다. 
>
> 즉, 사이즈가5인 큐라면 실제로 사용할 수 있는 공간은 4라는 점을 기억하셔야 합니다
>
> 리스트의 경우 스택과 마찬가지로 노드 클래스를 활용할 수 있습니다. 
>
> 차이점이 있다면 스택의 경우 pop부분에서 맨 앞자리의 원소를 빼기 위해 push부분에서 새로운 원소는 맨 앞자리에 추가했습니다.
>
> 반면, 이번 큐의 경우 dequeue부분에서 맨 앞자리의 원소를 빼기 위해 enqueue부분에서 새로운 원소는 맨 뒷자리에 추가합니다.


```python
class ArrayQueue:
    def __init__(self, init_size):
        self.mod_num = init_size
        self.front = 0
        self.rear = 0
        self.queue = []

    def init_queue(self):
        for _ in range(self.mod_num):
            self.queue.append(None)

    def enQueue(self, input_item):
        temp_index = (self.rear+1)%self.mod_num
        if temp_index == self.front:
            self.queue.insert(temp_index, input_item)
            self.mod_num += 1
            self.front += 1
            self.rear = temp_index
            # 큐의 상태를 출력하기 위한 코드입니다
            print("enqueue", input_item, self.queue)
            return
        self.rear = temp_index
        self.queue[temp_index] = input_item

        # 큐의 상태를 출력하기 위한 코드입니다
        print("enqueue", input_item, self.queue)

    def dequeue(self):
        if self.front == self.rear:
            return
        temp_index = (self.front+1)%self.mod_num
        self.front = temp_index
        item = self.queue[temp_index]
        self.queue[self.front] = None
        # 큐의 상태를 출력하기 위한 코드입니다
        print("dequeue", self.queue)
        return item


class Node:
    def __init__(self, data):
        self.next = None
        self.data = data


class ListQueue:
    def __init__(self):
        self.size = 0
        self.item = None

    def enQueue(self, input_item):
        if self.size == 0:
            self.item = Node(input_item)
        else:
            temp_node = self.item
            while temp_node.next is not None:
                temp_node = temp_node.next
            temp_node.next = Node(input_item)
        self.size += 1

    def deQueue(self):
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

print("=== Array queue ===")
queue1 = ArrayQueue(5)
queue2 = ListQueue()
queue1.init_queue()

queue1.enQueue(1)
queue1.enQueue(2)
queue1.enQueue(3)

queue1.dequeue()
queue1.dequeue()

queue1.enQueue(4)
queue1.enQueue(5)
queue1.enQueue(6)
queue1.enQueue(7)
queue1.enQueue(8)

queue1.dequeue()
print("==================")

print("=== List queue ===")
queue2.enQueue(1)
queue2.enQueue(2)
queue2.enQueue(3)
queue2.enQueue(4)
queue2.enQueue(5)

queue2.print_list()
print(queue2.deQueue())
print(queue2.deQueue())
print(queue2.deQueue())
print(queue2.deQueue())
print(queue2.deQueue())
print("==================")
```

```
출력예시
-------
=== Array queue ===
enqueue 1 [None, 1, None, None, None]
enqueue 2 [None, 1, 2, None, None]
enqueue 3 [None, 1, 2, 3, None]
dequeue [None, None, 2, 3, None]
dequeue [None, None, None, 3, None]
enqueue 4 [None, None, None, 3, 4]
enqueue 5 [5, None, None, 3, 4]
enqueue 6 [5, 6, None, 3, 4]
enqueue 7 [5, 6, 7, None, 3, 4]
enqueue 8 [5, 6, 7, 8, None, 3, 4]
dequeue [5, 6, 7, 8, None, None, 4]
==================
=== List queue ===
1 -> 2 -> 3 -> 4 -> 5 -> 
1
2
3
4
5
==================
```

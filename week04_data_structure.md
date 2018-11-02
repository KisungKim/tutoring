---
layout: default
title: "함수가 실행되는 과정에서 Stack자료구조를 엿볼 수 있는 코드"
---

> ## 함수가 실행되는 과정에서 Stack자료구조를 엿볼 수 있는 코드
> 파이썬으로 구현한 코드입니다.
>
> 다음의 script에서 볼 수 있는 것처럼 프로그램이 시작되고 차례로 func1과 func2를 부르게 됩니다. 
>
> 그러나 함수가 끝나는 순서는 func2, func1, main의 순서로 끝나게 됩니다.(SYSTEM 부분 참고)
>
> 이는 프로그램이 실행되면서 가상의 스택구조를 활용한다는 것을 의미합니다.
>

```python
stack_list = []


def print_info(n=None, data=None):
    return str("--------\n"+str(n)+"번째 함수, 현재 단계는 "+str(data)+"\n--------")


code_script = '''
def func2(data):
    print("SYSTEM : func2 started")
    new_data = data + 1
    return new_data


def func1(data):
    print("SYSTEM : func1 started")
    a, b = 1, 2 
    c = a+b + data 
    d = func2(c)
    print("SYSTEM : func2 ended")
 
    return d


def main():
    print("SYSTEM : program started")
    input_data = 2
    new_data = func1(input_data)
    print("SYSTEM : func1 ended")
    print("SYSTEM : program ended")


main()
'''

print("------- script started -------")
[print(line_number, each_line) for line_number, each_line in enumerate(code_script.split('\n'))]
print("------- script ended -------")

print("*********")
exec(code_script)
print("*********")

```

```
실행결과는 아래와 같이 나옵니다
-----
------- script started -------
0 
1 def func2(data):
2     print("SYSTEM : func2 started")
3     new_data = data + 1
4     return new_data
5 
6 
7 def func1(data):
8     print("SYSTEM : func1 started")
9     a, b = 1, 2 
10     c = a+b + data 
11     d = func2(c)
12     print("SYSTEM : func2 ended")
13  
14     return d
15 
16 
17 def main():
18     print("SYSTEM : program started")
19     input_data = 2
20     new_data = func1(input_data)
21     print("SYSTEM : func1 ended")
22     print("SYSTEM : program ended")
23 
24 
25 main()
26 
------- script ended -------
*********
SYSTEM : program started
SYSTEM : func1 started
SYSTEM : func2 started
SYSTEM : func2 ended
SYSTEM : func1 ended
SYSTEM : program ended
*********

Process finished with exit code 0

```

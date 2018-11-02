---
layout: default
title: "자바 클래스의 객체저장"
---

> ## 클래스의 객체저장
> 이전에 클래스 형변환 마지막 부분에서 부모와 자식클래스에 대해 설명했습니다.
>
> 자바 클래스의 경우 부모와 자식객체간 형변환은 가능하지만, 형제간의 형변환은 불가능합니다.
>

<br/>
위의 개념을 활용하면 부모 클래스를 활용한 배열에는(Animal class) 해당 부모와(Animal class) 자식객체를(Cat class, Dog class) 담을 수 있음을 볼 수 있습니다.
아래 예시를 통해 배열을 어떻게 다양한 형태로 선언할 수 있는지 그 방법에 대해 알아볼 수 있습니다.

##### 참고사항

<br/>
<code>instanceof</code> : 자바의 연산자, 어떤 객체의 클래스인지 boolean타입을(true/false) 리턴합니다. 여기서는 쉽게 말해 부모가 자식의 생활을 이해할 수 있는가? 라고 생각해주시면 됩니다.
<br/>
<br/>
<code>extends</code> : 상속의 개념입니다. 여기서는 쉽게 말해 '사람1 extends 사람2' 를 사람1은 사람2의 형질을 물려받았다(==사람1은 사람2의 자식이다) 라고 생각하셔도 됩니다.
<br/>
<br/>

```java

class Animal {
	public void action() {
		System.out.println("??? : Animal makes noise");
	}
}

class Dog extends Animal{
	
	@Override
	public void action() {
		System.out.println("Dog : woof woof");
	}
}

class Cat extends Animal{
	@Override
	public void action() {
		System.out.println("Cat : mew mew");
	}
}

public class Main {

	public static void main(String[] args) {
		System.out.println("========== Case 1 : 초기화에 대해서\n");
		Animal[] cage = new Animal[3]; // 초기화 방법 1
		cage[0] = new Animal();
		cage[1] = new Dog();
		cage[2] = new Cat();
		
		Animal[] cage2 = new Animal[]{new Cat(), new Dog(), new Animal()}; // 초기화 방법 2
		
		for (int i=0;i<cage.length;i++) {
			cage[i].action();
			cage2[i].action();
			System.out.println("-------");

		}
	}
}
```

```
실행결과는 아래와 같이 나옵니다
-----
========== Case 1 : 초기화에 대해서

??? : Animal makes noise
Cat : mew mew
-------
Dog : woof woof
Dog : woof woof
-------
Cat : mew mew
??? : Animal makes noise
-------

```

> ## for문 활용방법(1)
<br/>
<br/>
<code>for (int i=0;i<10;i++) </code> 처럼 index의 개념을 이용해, for 구문을 출력할 수도 있지만 
<br/>
아래와 같이 활용할 수도 있습니다.
<br/>

```java
class Animal {
	public void action() {
		System.out.println("??? : Animal makes noise");
	}
}

class Dog extends Animal{
	
	@Override
	public void action() {
		System.out.println("Dog : woof woof");
	}
}

class Cat extends Animal{
	@Override
	public void action() {
		System.out.println("Cat : mew mew");
	}
}

public class Main {

	public static void main(String[] args) {
		System.out.println("========== Case 1 : 초기화에 대해서\n");
		Animal[] cage = new Animal[3];
		cage[0] = new Animal();
		cage[1] = new Dog();
		cage[2] = new Cat();
		
		Animal[] cage2 = new Animal[]{new Cat(), new Dog(), new Animal()};
		
		for (int i=0;i<cage.length;i++) {
			cage[i].action();
			cage2[i].action();
			System.out.println("-------");

		}
		
		System.out.println("\n========== Case 2 : for문을 활용하는 방법(1)\n");
		for (Animal animal : cage) {
			animal.action();
		}
	}
}

```

```
실행결과는 아래와 같이 나옵니다
-----
========== Case 1 : 초기화에 대해서

??? : Animal makes noise
Cat : mew mew
-------
Dog : woof woof
Dog : woof woof
-------
Cat : mew mew
??? : Animal makes noise
-------

========== Case 2 : for문을 활용하는 방법(1)

??? : Animal makes noise
Dog : woof woof
Cat : mew mew

```

> ## instanceof 활용하기
<br/>
<br/>
교안에서 Cat 클래스의 reference를 Dog 클래스로, 혹은 그 반대의 경우 reference값을 연결할 수 없다고 설명합니다.
<br/>
아래와 같이 instanceof 연산자를 활용하면 Dog, Cat, Animal은 모두 Animal의 객체범주에 속하지만
<br/>
Dog의 객체범주에 속하는 클래스는 Dog 하나뿐임을 알 수 있고,
<br/>
그렇기 때문에 맨 위의 선언에서 <code>Dog[] cage = new Dog[3]</code> 가 아닌 <code>Animal[] cage = new Animal[3]</code>
<br/>
로 선언해야지만 그 자식클래스인 Dog와 Cat을 모두 담을 수 있음을 알 수 있습니다.
<br/>

```java

class Animal {
	public void action() {
		System.out.println("??? : Animal makes noise");
	}
}

class Dog extends Animal{
	
	@Override
	public void action() {
		System.out.println("Dog : woof woof");
	}
}

class Cat extends Animal{
	@Override
	public void action() {
		System.out.println("Cat : mew mew");
	}
}

public class Main {

	public static void main(String[] args) {
		System.out.println("========== Case 1 : 초기화에 대해서\n");
		Animal[] cage = new Animal[3];
		cage[0] = new Animal();
		cage[1] = new Dog();
		cage[2] = new Cat();
		
		Animal[] cage2 = new Animal[]{new Cat(), new Dog(), new Animal()};
		
		for (int i=0;i<cage.length;i++) {
			cage[i].action();
			cage2[i].action();
			System.out.println("-------");

		}
		
		System.out.println("\n========== Case 2 : for문을 활용하는 방법(1)\n");
		for (Animal animal : cage) {
			animal.action();
		}
		
		System.out.println("\n========== Case 3 : instanceof 로 뭐가 다른지 살펴보기 : Cat -> Dog가 불가능한 이유\n");
		for (Animal animal : cage) {
			if(animal instanceof Dog) {
				animal.action();
			}
		}
		System.out.println("-------");
		for (Animal animal : cage) {
			if(animal instanceof Animal) {
				animal.action();
			}
		}

	}

}
```

```
실행결과는 아래와 같이 나옵니다
-----
========== Case 1 : 초기화에 대해서

??? : Animal makes noise
Cat : mew mew
-------
Dog : woof woof
Dog : woof woof
-------
Cat : mew mew
??? : Animal makes noise
-------

========== Case 2 : for문을 활용하는 방법(1)

??? : Animal makes noise
Dog : woof woof
Cat : mew mew

========== Case 3 : instanceof 로 뭐가 다른지 살펴보기 : Cat -> Dog가 불가능한 이유

Dog : woof woof
-------
??? : Animal makes noise
Dog : woof woof
Cat : mew mew


```

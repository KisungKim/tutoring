---
layout: default
title: "자바 형변환에 대해 이해하기"
---

> ## 기본형의 형변환
> 자바에서 기본타입(primitive type)은 다른 기본 타입으로 변형될 수 있습니다.
>
> 이때 주의할 내용은 캐스팅이(형변환) 어떠한 방향으로 되는가 입니다.
>
> 예를 들어, 4bytes 크기의 자료를 담는 Integer을 8bytes 크기의 자료를 담는 double로 바꾼다고 합시다.

> 정수 3을 3.0으로 바꾼다

<br/>
byte의 단위를 물잔의 크기라고 한다면 작은 물잔에 들어있는 물(4bytes)을 큰 물잔에(8bytes) 옮기는데에는 큰 문제가 없습니다.
<br/>
반면 double의 값을 integer에 담을 때에는 *명시적* 으로 형을 변환해주어야 합니다.
<br/>
또한 예를 들어 3.4의 double값이라면 소수점 아래는 버려지는 모습을 살펴볼 수 있습니다.
<br/>
만약 같은 정수 자료형을 담는 long타입에서 integer타입으로의 형변환의 경우, 
<br/>
다시말해 long타입 변수가 integer가 표현할 수 있는 20억 이상의 숫자의 범위를 넘는 수일때(ex 50억)
<br/>
integer에는 long값이 그대로 들어가느 것이 아닌 trash값(개발자가 의도하지 않은 임의의 값)이 틀어가게 됩니다. 
<br/>
형변환은 다음의 예시를 통해 살펴볼 수 있습니다.

```java
public class Main {

	public static void main(String[] args) {

		double imEightBytes = 8.;
		int imFourBytes = 4;
		System.out.println("This is before casting : "+imEightBytes+" "+imFourBytes);
		
		// 아래는 암묵적으로(그러니까 자동적으로) 형변환이 이루어집니다.
		imEightBytes = imFourBytes;
		System.out.println("After casting, double value will be : "+imEightBytes);
		
		// Initialize
		imEightBytes = 8.3;
		// ==========

		// 아래 부분이 명시적으로 형변환이 이루어지는 부분입니다.
		imFourBytes = (int)imEightBytes;		
		System.out.println("After casting, integer value will be : "+imFourBytes);
```

```
실행결과는 아래와 같이 나옵니다
-----
This is before casting : 8.0 4
After casting, double value will be : 4.0
After casting, integer value will be : 8
```

> ## 클래스의 형변환
<br/>
<br/>
자바에서 기본타입(primitive type)은 다른 기본 타입으로 변형될 수 있다는 사실을 알아보았습니다.
<br/>
물론 개념은 다르지만 이와 유사한 방식으로 클래스간에도 형변환이 가능합니다.
<br/>
<br/>

> 간단히 말해 부모와 자식이 있다고 합시다.
>
> 자식은 아버지의 유전자를 물려받으면서 동시에 어머니의 유전자도 물려받기 때문에,
>
> 아버지와는 비슷하지만 또다른 성격을 보이게 됩니다.
>
> 그럼 이 경우 아버지는 어떻게 본인과는 다른 자식의 성격을 이해할 수 있을까요?

<br/>

##### 참고사항

<br/>
<code>instanceof</code> : 자바의 연산자, 어떤 객체의 클래스인지 boolean타입을(true/false) 리턴합니다. 여기서는 쉽게 말해 부모가 자식의 생활을 이해할 수 있는가? 라고 생각해주시면 됩니다.
<br/>
<br/>
<code>extends</code> : 상속의 개념입니다. 여기서는 쉽게 말해 '사람1 extends 사람2' 를 사람1은 사람2의 형질을 물려받았다(==사람1은 사람2의 자식이다) 라고 생각하셔도 됩니다.
<br/>
<br/>
<br/>

> 방금의 예시에서는 작은 그릇에 큰 그릇의 물을 담기에는 힘들어 명시적으로 형변환을 해주어야 한다고 했습니다. 
> 
> 이번의 경우는 다릅니다. 부모는 자식보다 경험이 많아 따로 형변환 없이도 
>
> 자식의 성격을 쉽게 알 수 있다고 생각해주시면 됩니다.(암묵적 형변환) 
> 
> 대신 instanceof 연산자를 통해 이 아버지가 자식을 이해하는 아버지인지 자식을 이해하지 못하는 아버지인지 확인할 수 있겠죠.
> 
> 위의 개념은 이후에 상속에서 좀 더 많이 쓰이게 될 것입니다.

<br/>

```java
class Father {
	
	void whoAmI() {
		System.out.println("I'm father class");
	}
}

class Son extends Father {
	
	@Override
	void whoAmI() {
		System.out.println("I'm son class");
	}
	
}


public class Main {

	public static void main(String[] args) {

		Father imFatherClass = new Father();
		Son imSonClass = new Son();
		
		imFatherClass.whoAmI();
		
		System.out.println("Before Type casting, is isFatherClass instance of Son? : "+String.valueOf(imFatherClass instanceof Son));
		System.out.println("Before Type casting, is isFatherClass instance of Father? : "+String.valueOf(imFatherClass instanceof Father));

		imFatherClass = imSonClass;
		imFatherClass.whoAmI();
		
		System.out.println("After Type casting, is isFatherClass instance of Son? : "+String.valueOf(imFatherClass instanceof Son));
		System.out.println("After Type casting, is isFatherClass instance of Father? : "+String.valueOf(imFatherClass instanceof Father));

	}
}


```

```
실행결과는 아래와 같이 나옵니다
-----
I'm father class
Before Type casting, is isFatherClass instance of Son? : false
Before Type casting, is isFatherClass instance of Father? : true
I'm son class
After Type casting, is isFatherClass instance of Son? : true
After Type casting, is isFatherClass instance of Father? : true

```

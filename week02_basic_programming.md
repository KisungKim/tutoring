---
layout: default
title: "자바 클래스에 대해 이해하기"
---

> method영역, heap영역, stack영역

다음의 글을 참고하셔도 도움이 됩니다
<br/>
<a href="http://programmer-seva.tistory.com/72">참조 타입과 메모리</a>
<br/>
정말 간단하게 말하면 <code>public static void main(String args[]) { } </code>라는 놈이 <b>만들어진 프로그램의 시작</b>(엄밀히 말하면 아닙니다)이라고 생각하시면 됩니다.
<br/>
그리고 위 메소드는 stack영역에서 실행됩니다.
<br/>
일단 stack영역에서 실행이 되고 만약 main함수에서 <code>Car myobj = new Car();</code>와 같이 객체를 생성했다면,
<br/>
method영역에서 Car클래스의 정보를 가져와서 heap영역에 myobj를 마련한다고 생각하시면 됩니다.
<br/>
그냥 여기서는 

1. 프로그램이 돌아가는 <b>순서</b>, == stack영역 ex> public static void main(String args[])
2. 프로그램이 돌아가면서 <b>사용하는 클래스의 정보</b>, == method영역 ex> class 'Car'
3. 프로그램이 돌면서 생성한 <b>객체들의 정보가</b> == heap영역 ex> instance 'myobj'

각각 구분되어 저장된다고만 이해하시면 됩니다.

> 자바 클래스의 생성자 이해하기

## 생성자란?

<br/>
자바 클래스는 기능적인면에서 패키지, import모듈, 필드, 생성자, 메소드로 이루어져 있습니다.
<br/>
import모듈의 경우 일단 지금은 설명을 생략하겠습니다. 
<br/>
패키지의 경우 이전 튜터링 파일을 참고하시면 됩니다.
<br/>
생성자의 경우 자동차 공장에서의 생산라인이라고 생각하시면 됩니다.
<br/>
코드상에서 클래스 이름과 같은 메소드를 가집니다.

```java
class Car {
  // ...(중략)...
  public Car() {};                // <- 이런 놈들이
  public Car(int something) {};   // <- 생성자입니다.
  // ...(중략)...
}
```

<br/>
자동차 공장, 즉 Car이라는 이름을 가진 class가 있을 때 
<br/>
그 공장 안에는 여러 생산라인이 있습니다.
<br/>
예를 들어 기본적으로 빨간색 자동차만 생산하는 생산라인, 혹은 기본적으로 DIY자동차를 생산하는 생산라인, 혹은 기본적으로 아반x만 생산하는 생산라인, 혹은 그냥 박스형 자동차만 생산하는 생산라인이 있을 수 있습니다.
<br/>
이를 생성자의 개념에 대입해보면..

1. 기본적으로 빨간색 자동차만 생산하는 생성자
2. 기본적으로 DIY 자동차만 생산하는 생성자
3. 기본적으로 아반x 자동차만 생산하는 생성자
4. 아무것도 정해지지 않은, 기본형 자동차만 생산하는 생성자

로 정리해 볼 수 있습니다.

### 기본적으로 빨간색 자동차만 생산하는 생성자

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 기본적으로 DIY 자동차만 생산하는 생성자

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 기본적으로 아반x 자동차만 생산하는 생성자

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 아무것도 정해지지 않은, 기본형 자동차만 생산하는 생성자

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 그럼 위를 모두 포함하는 Car 자동차 공장(class)의 경우 다음과 같이 표현이 가능합니다.

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 그러면 저희는 main Class에서 다음과 같이 자동차를 만들어 줄 수 있습니다.

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

## 메소드란?

이전에 생성자를 자동차의 생산라인이라고 비유했습니다.
<br/>
매소드는 쉽게 말해 그렇게 만들어진 자동차를 출하할 때, 혹은 생성 과정에서 어떤 활동을 할것이냐 라는 '행동'을 정의해 줍니다.
<br/>
두 가지의 예를 들자면, 출하 후 소비자에게 만들어진 차의 정보를 보여주는 행동과 일반 자동차를 고객의 요구에 맞게 공장에서 자동차를 다시 제조하는 행동을 생각할 수 있습니다. 

1. 출하 후 소비자에게 만들어진 차의 정보를 보여주는 메소드
2. 일반 자동차를 고객의 요구에 맞게 공장에서 자동차를 다시 제조하는 메소드

### 출하 후 소비자에게 만들어진 차의 정보를 보여주는 메소드

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 일반 자동차를 고객의 요구에 맞게 공장에서 자동차를 다시 제조하는 메소드

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 그럼 위를 모두 포함하는 Car 자동차 공장(class)의 경우 다음과 같이 표현이 가능합니다.

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

### 그러면 저희는 main Class에서 다음과 같이 메소드를 사용할 수 있습니다.

```java
class이름 인스턴스이름 = new class이름();
예를 들어.. 된장국을
Cooking duenjang = new Cooking();
이런식으로 만들어 줄 수 있습니다.
```

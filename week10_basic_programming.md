---
layout: default
title: "자바기본개념(toString, equals, 다형성, 상속에서의 접근제한자)"
---
 
> ### toString()메소드에서 super()의 의미와 toString()메소드를 사용하는 이유는 무엇입니까?
>
> toString의 경우 String이라는 자바 라이브러리 클래스 내에 이미 정의되어있는 메소드입니다. 
>
> 원래 toString()은 해당 객체에 대한 정보를 String type으로 리턴하는 역할을 합니다. 
>
> 기본적으로 출력되는 값은 해당 객체의 정보를 리턴한 값이기 때문에 예를 들어 edu.skky.ccc.Cal@70dea4e는 
>
> edu.skky.ccc.Cal이라는 패키지의 70dea4e라는 가상이름을 가진 객체라는 의미입니다. 
>
> 그런데 각 클래스마다 해당 객체에 대한 정보를 다르게 보여주고 싶은 경우가 있습니다. 
>
> 예를 들어 Student라는 클래스를 만들었을 때, 그 가상이름보다는 Student 클래스 내부의 stuId나, stuName등을 
>
> 보여주고 싶은 경우인데, 그때는 재정의인 override를 통해 본래 toString이 아닌, stuId등을 출력하는 메소드로 
>
> 사용자가 바꿔주는 겁니다. 그래서 super.toString의 경우 사용자가 바꾸기 전 원래 toString의 출력값을 
>
> 보여주고(패키지명+가상이름) 그 이후의 값은 사용자가 출력하기를 원하는 값으로 바꾸는 모습을 보여주는 겁니다

> ### clone에 대해 잘 이해가 가지 않습니다. clone을 사용하기 위해서는 반드시 try-catch구문을 사용해야 하는건가요?
>
> clone의 경우는 저도 사용해보지를 않았습니다만, 아마 자바 내부에서 객체를 복제하는데 오류가 발생하는 경우가 있는 것 같습니다. 
>
> 흔히 file을 open하는 코드에서 IOException을 예외로 걸어주는 것처럼 clone시에도 항상 예외오류가 
>
> 발생할 가능성이 있어 무조건 try-catch를 적어주셔야 하는것 같습니다.

> ### equals의 경우에는 항상 boolean을 리턴하도록 지정을 해주어야 하나요?
> equals도 toString의 예시와 마찬가지로 Object 클래스에서 이미 정의된 equals와 String 클래스에서 
>
> 이미 정의된 equals가 있습니다. 전자의 경우 해당 객체의 가상 주소값(쉽게 말해 같은 객체인지 아닌지를 비교)를 비교하는거고 
>
> 후자의 경우 문자열이 같은지를 비교하는 겁니다. String의 경우 equals가 아닌 그낭 ==를 사용했을 때에는 
>
> Object클래스의 equals가 사용되어 객체의 주소값을 비교하므로 같은 문자열이라도 객체가 다르다면 false를 리턴하게 됩니다. 
>
> Object클래스의 equals를 오버라이드한경우에만 boolean을 리턴하도록 지정을 해주어야 하며 그 이외의 경우에는 
>
> 상황에 따라 적어주시면 됩니다.

> ### 상속의 경우 접근제한자에 대해 설명해 주세요.
> 상속을 할 때에는 부모가 선언한 접근제한자보다 같거나 더 넓은 범위를 허용해 주어야 합니다. 
>
> 예를 들어, 부모의 클래스에서 public으로 어떤 추상메소드를 선언한 경우 private-default-protected-public에 따라 
>
> 자식 클래스에서 해당 메소드를 재정의할 때에 public이외의 접근제한자는 사용할 수 없습니다

> ### 다형성에 대해서 잘 이해가 가지 않습니다.
> 보통 new로 객체가 생성될 때, 원래는 super()이라는 키워드가 생성자에 명시되어 있지 않아도 항상 super을 호출합니다. 
>
> 이 말은 예를 들어서 Car이라는 클래스가 있다고 가정하면 최상위 클래스인 Object클래스부터 Car사이에 해당하는 
>
> 모든 클래스를 다 호출하고 맨 마지막에 Car class의 생성자를 호출한다는 의미가 됩니다. 
>
> 이때 Object a = new Car(); 처럼 선언할 수도 있는데 위처럼 선언하는 이유로는 공통된 부모를 상속받는 클래스로 
>
> 객체를 선언했을때, 같은 자료구조에 묶일 수 있고(ex Object[]), 그걸 꺼내는 상황에서 실제로 필요한 상황에 
>
> 특정 객체인지 확인하고 각 객체의 특징에 따라 메소드를 호출하고 활용하기 위함입니다. 
>
> 자세한 내용은 아래 코드를 참고하시면 됩니다. 

```java
class Car {
	public Car() {
	}

	void basic() {
	}
}

class Avante extends Car {
	int num;
	public Avante(int input) {
		num = input;
		System.out.println("init B ended "+num);
	}
	void option() {
		System.out.println("Avante "+num);
	}
}

class BMW extends Car {
	int num;
	public BMW(int input) {
		num = input;
		System.out.println("init B ended "+num);
	}
	void option() {
		System.out.println("BMW "+num);
	}
}

public class IFaceTest {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Car a1 = new BMW(3);
		Car a2 = new Avante(4);
		
		Car[] aCar = {a1, a2};
		for(int i=0;i<aCar.length;i++) {
			if (aCar[i] instanceof BMW) {
				((BMW)aCar[i]).option();				
			} else if (aCar[i] instanceof Avante) {
				((Avante)aCar[i]).option();				
			}
		}
		
		Object a = new String("car");
		System.out.println(a.toString());
		Object b = new Object();
		System.out.println(b.toString());
		
	}

}
```

```
출력결과
==========
init B ended 3
init B ended 4
BMW 3
Avante 4
car
java.lang.Object@4e25154f
```

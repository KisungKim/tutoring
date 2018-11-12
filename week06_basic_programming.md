---
layout: default
title: "2차원 배열의 활용(입문)"
---

> ## 2차원 배열의 활용(입문) 예제
> TODO 부분을 완성해주시면 됩니다
>
> 주석과 예시를 자세하게 적었으니 Readme 및 예시, TODO를 잘 참고해 주세요
> main클래스 내부만 작성해주시면 됩니다

```java
public class Main {

	public static void main(String[] args) {
		/* README
		 * Description >  
		 * air code: air condition
		 * 
		 * Example >  
		 * 0: sunny 
		 * 1: cloud 
		 * 2: mist 
		 * 3: rain 
		 * */ 
		int[][] airTable = {
		//(열번호 0  1  2  3  4  5  6) 
		// 일차   1  2  3  4  5  6  7
                        {0, 0, 0, 1, 2, 3, 3}, // korea(행번호 0)
                        {0, 1, 2, 2, 2, 3, 0}, // japan(행번호 1)
                        {2, 2, 3, 3, 0, 0, 0}, // china(행번호 2)
                        {2, 2, 2, 1, 1, 1, 3}, // france(행번호 3)
		};
		// ex> airTable[0][1]은 korea의 2일차 날씨를 나타냅니다
				
		/*
		 * TODO: 주어진 airTable의 air code를 토대로 
		 * 국가별(이차원배열의 행) air condition을 일자별로(이차원배열의 열) 출력하는 코드를
		 * loop구문 및 if구문을 적절히 활용하여 구현하세요.
		 */
	}
}
```

```java
// 이해를 돕기 위한 예시코드 ======================
// 예를 들어 위의 airTable에서 4일차의 france의 날씨는 cloud입니다(날씨코드 1)
// 그렇다면 아래와 같이 작성하여 출력할 수 있습니다
int countryCode=3; // 이차원배열의 열의 index가 0부터 시작하므로 4번째 국가인 france의 index는 3입니다
int day=3; // 이차원배열의 행의 index가 0부터 시작하므로 4일차의 index는 3입니다
  System.out.println(airTable[countryCode][day]);
if(airTable[countryCode][day] == 0) {
  System.out.println("sunny");
} else if(airTable[countryCode][day] == 1) {
  System.out.println("cloud");
}
// ============================================ 
```

> 목표 출력
```
  1 일차
kor : sunny
japan : sunny
china : mist
france : mist
  2 일차
kor : sunny
japan : cloud
china : mist
france : mist
  3 일차
kor : sunny
japan : mist
china : rain
france : mist
  4 일차
kor : cloud
japan : mist
china : rain
france : cloud
  5 일차
kor : mist
japan : mist
china : sunny
france : cloud
  6 일차
kor : rain
japan : rain
china : sunny
france : cloud
  7 일차
kor : rain
japan : sunny
china : sunny
france : rain
```

> 답안
```java
public class Main {

	public static void main(String[] args) {
		/* README
		 * Description >  
		 * air code: air condition
		 * 
		 * Example >  
		 * 0: sunny 
		 * 1: cloud 
		 * 2: mist 
		 * 3: rain 
		 * */ 
		
		int[][] airTable = {
		//(열번호 0  1  2  3  4  5  6) 
		// 일차   1  2  3  4  5  6  7
				{0, 0, 0, 1, 2, 3, 3}, // korea(행번호 0)
				{0, 1, 2, 2, 2, 3, 0}, // japan(행번호 1)
				{2, 2, 3, 3, 0, 0, 0}, // china(행번호 2)
				{2, 2, 2, 1, 1, 1, 3}, // france(행번호 3)
		};
		// ex> airTable[0][1]은 korea의 2일차 날씨를 나타냅니다
				
		/*
		 * TODO: 주어진 airTable의 air code를 토대로 
		 * 국가별(이차원배열의 행) air condition을 일자별로(이차원배열의 열) 출력하는 코드를
		 * loop구문 및 if구문을 적절히 활용하여 구현하세요.
		 */
		int countryCode;
		int day;
		for(day=0;day<airTable[0].length;day++) {
			System.out.println("  "+(day+1)+" 일차");
			countryCode=0;
			while(countryCode<airTable.length) {
				String airCondition = "";
				if (airTable[countryCode][day] == 0) {
					airCondition = "sunny";
				} else if (airTable[countryCode][day] == 1) {
					airCondition = "cloud";
				} else if (airTable[countryCode][day] == 2) {
					airCondition = "mist";
				} else {
					airCondition = "rain";
				} 
				
				String countryName = "";
				if (countryCode==0) {
					countryName = "kor";
				} else if (countryCode==1) {
					countryName = "japan";					
				} else if (countryCode==2) {
					countryName = "china";					
				} else {
					countryName = "france";					
				}
				System.out.println(countryName+" : "+airCondition);
				countryCode++;
			}
		}

	}

}

```
	

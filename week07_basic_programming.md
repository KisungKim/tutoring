---
layout: default
title: "pseudo 코드에서부터 실전 코드까지 구현(Simple Dot Com instance와 유사)"
---

> ## pseudo 코드에서부터 실전 코드까지 구현(Simple Dot Com instance와 유사)
> 

```java
package com.skku.java.tutoring09;

import java.util.Scanner;

public class Game {

	public static void main(String[] args) {
		// TODO : 아래는 큰 단의 flow입니다
		// 게임 이름 : 마피아를 찾아라
		// 1. 7명 중 3명이 마피아이다.						=> 7명의 사람을 크기가 7인 int 배열로 선언하겠다, 그 중 3개는 특정 값을 가진다.
		// ex > 일반인, 일반인, 일반인, 일반인, 마피아, 마피아, 마피아
		// 2. 마피아의 위치는 변하지 않는다					=> int 배열에서 각 index의 int 값은 변하지 않는다
		// 3. 마피아의 위치를 알아 맞추면 마피아는 죽는다			=> 사용자가 특정 index를 알아맞추면 프로그램은 특정한 메시지를 출력한다
		// 4. 모든 마피아가 죽을 때까지 게임은 계속된다			=> 3개의 특정 index를 모두 알아맞추기 전까지 loop는 반복된다
		// 5. 모든 마피아가 죽으면 'finished'를 출력한다		=> 3개의 특정 index를 모두 알아맞추면 'finished'를 출력한다
		
		
		// TODO : 아래는 psudo code입니다
		// 1. 크기가 7인 int 배열을 선언
		// 2. int배열에서 3개는 값 -1로, 나머지는 1로 채움(마피아의 위치와 일반 사람들의 위치 초기화)
		// 3. 사용자가 죽인 마피아의 수 cnt로 초기화
		// 4. loop 시작
		// 5. 	사용자가 특정 값을 제시
		// 6. 	특정 값의 인덱스가 -1인지 확인
		// 7. 		특정 값의 인덱스가 -1인 경우,
		// 8. 			해당 인덱스의 값을 0으로 바꿈
		// 9. 			cnt의 값을 증가시킴
		// 10. 				만약 cnt값이 3이라면 게임 종료
		// 11. 			다시 루프로 되돌아감
		// 12. 		특정 값의 인덱스가 -1이 아닌경우, 	
		// 13.			다시 루프로 되돌아감 	
		
		
		// TODO : 아래는 실전코드 입니다
		Scanner sc = new Scanner(System.in);
		// 1. 크기가 7인 int 배열을 선언
		int[] people = new int[7];
		// 2. int배열에서 3개는 값 -1로, 나머지는 1로 채움(마피아의 위치와 일반 사람들의 위치 초기화)
		people[0] = 1; people[1] = 1; people[2] = 1; people[3] = 1; people[4] = -1; people[5] = -1; people[6] = -1;
		// 3. 사용자가 죽인 마피아의 수 cnt로 초기화
		int cnt = 0;
		// 4. loop 시작
		while(true) {
			System.out.println("입력하세요 0에서 7의 숫자");
			// 5. 사용자가 특정 값을 제시
			int now = Integer.parseInt(sc.nextLine());
			// 6. 특정 값의 인덱스가 -1인지 확인
			// 7. 특정 값의 인덱스가 -1인 경우,
			if (people[now] == -1) {
					// 8. 해당 인덱스의 값을 0으로 바꿈
					people[now] = 0;
					System.out.println("hit!");
					// 9. cnt의 값을 증가시킴
					cnt++;
					// 10. 만약 cnt값이 3이라면 게임 종료
					if(cnt==3) {
						System.out.println("finished!!");
						return;
					}
					// 11. 다시 루프로 되돌아감
					continue;
			}
			// 12. 특정 값의 인덱스가 -1이 아닌경우, 
			else {
				// 13. 다시 루프로 되돌아감 	
				continue;
			}
		}
	}
}

```

> 출력
```
입력하세요 0에서 7의 숫자
1
입력하세요 0에서 7의 숫자
4
hit!
입력하세요 0에서 7의 숫자
5
hit!
입력하세요 0에서 7의 숫자
6
hit!
finished!!

```
